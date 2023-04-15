## Uploading both Multipart File and Request Body using Spring Rest Template

Suppose we have to design a REST endpoint that accept an file attachment and a request body JSON both. We have to call this end point using Spring RestTemplate.

Lets suppose 
* We have to upload an excel file as attachment and 
* Request body JSON for an Employee as below

```sh
{
  "id" : 123,
  "name": "Vks"
} 
```

In Java class we will use MultipartFile class for attachment and Employee class as model for the json.
Content Type for attachment will be - MediaType.MULTIPART_FORM_DATA in this case. We can choose MediaType according to type of attachment. For request body JSON media type will be MediaType.APPLICATION_JSON.

Below is the method for the same.

```sh
void restCallWithAttachmentAndData(MultipartFile file) throws IOException{
		
		MultiValueMap<String,Object> multipartRequest = new LinkedMultiValueMap<>(); 
        
		//HttpHeaders for Attachment
		HttpHeaders requestHeadersAttachment = new HttpHeaders();
		requestHeadersAttachment.setContentType(MediaType.MULTIPART_FORM_DATA);
		
		ByteArrayResource fileAsResource = new ByteArrayResource(file.getBytes()){
		    @Override
		    public String getFilename(){
		        return file.getOriginalFilename();
		    }
		};
		HttpEntity<ByteArrayResource> fileAttachmentment 
		              = new HttpEntity<>(fileAsResource,requestHeadersAttachment);
		multipartRequest.set("file",fileAttachmentment);

        //HttpHeader for JSON data
		HttpHeaders requestHeadersJSON = new HttpHeaders();
		requestHeadersJSON.setContentType(MediaType.APPLICATION_JSON);
		
		Employee employee = new Employee();
		employee.setId(123);
		employee.setName("Vks");
		
		HttpEntity<Employee> requestEntityJSON 
		                 = new HttpEntity<>(employee, requestHeadersJSON);
		multipartRequest.set("emp",requestEntityJSON);
		
		//Main request HttpHeaders
		HttpHeaders requestHeaders = new HttpHeaders();
		requestHeaders.setContentType(MediaType.MULTIPART_FORM_DATA);

		HttpEntity<MultiValueMap<String,Object>> requestEntity 
		                 = new HttpEntity<>(multipartRequest,requestHeaders); 

		ResponseEntity<String> response = restTemplate.exchange("http://localhost:8080/upload/emp",
				HttpMethod.POST,
				requestEntity,
				String.class);
		
	}
	
```


On Server side, in Controller class we will use **@RequestPart** annotaion to accept the data. 

```sh
@PostMapping("/upload/emp")
	public ResponseEntity<String> upload(@RequestPart("emp") Employee employee,
			@RequestPart("file") MultipartFile file ){
		
		// Other code  
		return ResponseEntity.status(HttpStatus.OK).body("Got Request...");
		
	}

```