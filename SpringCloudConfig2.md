
# Spring Cloud Config


# Spring Cloud Config Server 

```java

@SpringBootApplication
@EnableConfigServer
public class SpringCloudConfigServerApplication {

	public static void main(String[] args) {
		SpringApplication.run(SpringCloudConfigServerApplication.class, args);
	}

}

```

application.properties/yml

>spring.cloud.config.server.git.uri: path/to/git/repo



# Spring Cloud Config Client

application.properties/yml

>spring.config.import=optional:configserver:http://localhost:8888

Access properties from Config server in your application as-

```java

@RestController
public class MyController {
	
	@Value("${app.message: This default value of message}")
	private String message;
	
	@GetMapping("/message")
	public String getMessage() {
		return "app.message = " + message;
	}
}

```



