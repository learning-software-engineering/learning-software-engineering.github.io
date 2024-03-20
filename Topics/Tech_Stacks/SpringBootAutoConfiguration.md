# Auto Configuration in SpringBoot
## Introduction
Auto-configuration in Spring Boot is a pivotal feature, designed to simplify application development by automatically configuring Spring Beans based on the application's dependencies and configuration. This feature is realized through conditional configurations, meaning configurations are applied only under specific conditions, such as the presence of certain dependencies, configuration values, or environment variables.

Spring Boot includes several "Starter" packages, which bundle a set of default dependencies and configurations to ensure the smooth running of an application. For instance, the Spring Boot Starter Web package adds dependencies and configurations for Spring MVC, Tomcat, and other web-related features, enabling auto-configuration of web settings when this starter is included.

The essence of Spring Boot auto-configuration lies in dependency injection. This mechanism automatically injects required dependencies into beans, eliminating the need for manual configuration code. By simply adding the appropriate dependencies to the pom.xml file and configuring properties in application.yml, Spring Boot takes over the configuration process, making the required beans available in the Spring IoC (Inversion of Control) container through dependency injection.
## @SpringBootApplication Annotation
The @SpringBootApplication annotation is a convenience annotation that adds all of the following:
- @SpringBootConfiguration: Marks the class as a configuration class.
- @EnableAutoConfiguration: Enables Spring Boot's auto-configuration mechanism.
- @ComponentScan: Tells Spring to scan for components.
### Example
#### @SpringBootConfiguration
Principle: Acts as a specialization of `@Configuration`, marking the class as a source of bean definitions.

Mechanism: When the application starts, Spring Boot scans for classes annotated with `@SpringBootConfiguration` to construct the application context. It is treated as the primary configuration class and serves as an entry point for further configuration and component scanning.

Handler: The handling of `@SpringBootConfiguration` is managed by the Spring Framework's `ConfigurationClassPostProcessor`. This processor scans for `@Configuration` classes (and by extension `@SpringBootConfiguration` classes) and processes them to register bean definitions contained within those classes.
An example of a simple configuration that could be applied within an application marked by `@SpringBootConfiguration`:
```Java
@SpringBootConfiguration
public class MyConfiguration {

    @Bean
    public SomeService someService() {
        return new SomeServiceImpl();
    }
}
```
#### @EnableAutoConfiguration
Principle: @EnableAutoConfiguration tells Spring Boot to start adding beans based on classpath settings, other beans, and various property settings. This annotation is perhaps the most pivotal in the auto-configuration process. It leverages Spring's `@Import` annotation to register additional configurations. The key handler for this annotation is the `AutoConfigurationImportSelector`, which implements the `ImportSelector` interface.

Mechanism: 
1. Starting Phase (of the container): When a Spring Boot application starts, it begins by creating an `ApplicationContext`. This context is then prepared and refreshed. During this phase, the `SpringApplication` class plays a crucial role in bootstrap operations, including the application context initialization and the execution of the auto-configuration process.
2. The `@SpringBootApplication` annotation is usually placed on the main class. This annotation encompasses `@SpringBootConfiguration`, `@EnableAutoConfiguration`, and `@ComponentScan`.
3. The `AutoConfigurationImportSelector` Mechanism: When processing `@EnableAutoConfiguration`, the `AutoConfigurationImportSelector` is invoked. This selector's job is to determine which auto-configuration classes should be imported based on the conditions present at runtime. It does this in several steps:
- Select Imports: The `selectImports` method of `AutoConfigurationImportSelector` is called by Spring Framework during the application context initialization phase. This method is responsible for returning the names of auto-configuration classes to be registered.
- Load Conditionally: The selector loads the candidates for auto-configuration from the `META-INF/spring.factories` files found within the classpath. Each entry in these files is considered if its condition matches (using `@Conditional` annotations on the auto-configuration classes).
- Register Bean Definitions: Once the conditions are evaluated, and the classes are selected, their bean definitions are registered in the  `ApplicationContext`. The actual instantiation of beans from these definitions will occur based on the usual Spring Framework lifecycle, ensuring that dependencies are injected, and configurations are applied as expected.

Handler: The `AutoConfigurationImportSelector` is the main handler for @EnableAutoConfiguration. As metioned in mechanism part, it selects and imports auto-configuration classes during the application's startup. This import selector uses the `SpringFactoriesLoader` mechanism to locate and load auto-configuration classes.

Imagine you have a Spring Boot application with the following main class:
```Java
@SpringBootApplication
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }
}
```
The `@SpringBootApplication` annotation includes `@EnableAutoConfiguration`. Suppose you have added the spring-boot-starter-web dependency to your project. In one of the `spring.factories` files within this starter, you might find an entry like:
```properties
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
org.springframework.boot.autoconfigure.web.servlet.WebMvcAutoConfiguration
```

During the startup, `AutoConfigurationImportSelector` reads this entry and checks if the conditions for the `WebMvcAutoConfiguration` class are met (e.g., if specific classes are present on the classpath). If the conditions are satisfied, `WebMvcAutoConfiguration` is imported, effectively setting up Spring MVC with default settings for your application without requiring explicit configuration.

This mechanism, powered by `@EnableAutoConfiguration` and handled through `AutoConfigurationImportSelector`, significantly simplifies Spring application development by automatically configuring beans based on the environment and classpath.

#### @ComponentScan
`@ComponentScan` tells Spring where to look for annotated components/classes.

Mechanism: During the application startup, Spring Framework's  `ClassPathBeanDefinitionScanner` scans for classes annotated with stereotypes like `@Component`, `@Service`, `@Repository`, etc., within the specified base packages. This process involves locating, loading, and registering bean definitions.

Handler: The `ComponentScanAnnotationParser` is responsible for parsing `@ComponentScan` annotations and configuring the `ClassPathBeanDefinitionScanner` accordingly. This scanner then registers the discovered beans in the Spring Application Context.

```Java
@SpringBootApplication
@ComponentScan(basePackages = "com.example.myapp")
public class MyApp {
    // ...
}
```
## Conclusion
Spring Boot's auto-configuration simplifies application development by automatically setting up configurations based on the application's needs and context. It's implemented through a combination of annotations and conditional logic, primarily driven by the `@EnableAutoConfiguration` annotation and the SpringFactories mechanism. This approach allows developers to rapidly develop and deploy Spring applications, making Spring Boot a favored framework for modern Java application development.
