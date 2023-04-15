Spring Cloud Configuration


# Spring Cloud Config

![Arch](file:///D:/Vik/Study/MD%20Files/Images/SpringCloudConfigArch.png)

# Spring Cloud Config Server

__pom.xml__
```
    <dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-config-server</artifactId>
	</dependency>
``` 

```java

@SpringBootApplication
@EnableConfigServer
public class SpringCloudConfigServerApplication {

	public static void main(String[] args) {
		SpringApplication.run(SpringCloudConfigServerApplication.class, args);
	}

}

```

__application.properties/yml__
```
spring.cloud.config.server.git.uri: path/to/git/repo
```



# Spring Cloud Config Client

__pom.xml__

```sh
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-config</artifactId>
		</dependency>
```

__application.properties/yml__
```
spring.config.import=optional:configserver:http://localhost:8888
```

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