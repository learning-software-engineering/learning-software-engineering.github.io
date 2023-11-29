# Managing Environment Variables and Secrets

## Introduction

In this guide, we'll explore how to effectively manage environment variables and secrets. This is crucial for maintaining security and flexibility in different environments like development, testing, and production. We will be using the Spring framework as a running practical example.

## Table of Contents
- [Introduction](#introduction)
- [Understanding Environment Variables](#what-are-environment-variables)
- [Securing Secrets](#securing-secrets)
- [Switching Environments](#switching-environments)
- [Best Practices](#best-practices)

## What Are Environment Variables?

Environment variables are dynamic-named values that can affect the way running processes will behave on a computer. Environment variables are usually loaded into the application at runtime, and are loaded from the environment in which the application is being run.

We may choose to use environment variables over global variables for various reasons. For instance:

- **Configuration:** Some variables hold values that need to be configured based on the use case. We can change environment variables without making changes to the code itself.
- **Continuous Integration/Deployment:** In CI/CD pipelines, environment variables can be set dynamically for each stage (build, test, deploy).
- **Independence Between Instances:** Environment variables enable you to manage configurations for multiple instances of the same application.
- **Adapting to Different Environments:** Environment variables allow for different behavior in different environments (development, staging, production) without making code changes.
- **Security Compliance:** Security standards and regulations recommend or require the use of environment variables to handle sensitive data.
- **Reducing Risk of Accidental Exposure:** Environment variables remove the risk of accidentally exposing secrets through source code repositories or other shared resources. (I had personally done this when initially setting up my repo)!
- **Local Development:** We can set our own local environment variables without changing code, making it easier to work on the application without altering shared settings.

Environment variables are typically defined in the environment or stored in a local `.env` file. We load these into our application at runtime by either manually parsing the variables or using a built-in feature of a framework. In Spring, for example, we can load in environment variables through our `application.properties` file:

```java
# URLs
backend.url=${BACKEND_URL}
frontend.url=${FRONTEND_URL}
```

The environment variables are those surrounded by the `${}` identifier. We can later use these variables in the code - for example 

```
@Value("${backend.url}")
private String backendUrl;
```

## Securing Secrets

As per the sneak peak above, it is common practice to store secrets as environment variables rather than in the application code or property files directly. We will take a look at why this is the case.

Let us consider a class `JwtTokenProvider` which uses a predefined `jwtSecret` to generate tokens. We could take the naive approach:

```java
@Component
public class JwtTokenProvider {
    private String jwtSecret = "Top Secret Key";

    public String generateToken(String userId) {
        Date now = new Date();
        Date expiryDate = new Date(now.getTime() + jwtExpirationMs);

        return Jwts.builder()
                .setSubject(userId)
                .setIssuedAt(now)
                .setExpiration(expiryDate)
                .signWith(Keys.hmacShaKeyFor(jwtSecret.getBytes()))
                .compact();
    }
}
```

A couple of issues could arise here. Firstly, any access to the source code (directly or indirectly, perhaps through reverse engineering) would reveal our top secret `jwtSecret`. In addition, we may require a different secret for each environment. Not only is this approach insecure, it is also inconvenient! 

We may decide to decouple the value of this key from the code and instead leave it configurable in a properties file. For example, our property file would now contain:

```
app.jwtSecret=Top Secret Key
```

We will also change the class to grab this key from our properties that are loaded in at runtime by using our Spring annotation:

```
@Value("${app.jwtSecret}")
private String jwtSecret;
```

Sadly, this approach does not really solve our security concerns. The secret is still very much visible in the source code! We solve this problem by loading our environment with the environment variable. For example, we could run the following on a Linux box:

```
nosnow-user@Kiyosaki: export JWT_SECRET="Top Secret Key"
nosnow-user@Kiyosaki: echo $JWT_SECRET
Top Secret Key
```

Lastly, we can rest easy knowing that our key no longer resides in our code by modifying our `application.properties` file:

```
app.jwtSecret=${JWT_SECRET}
```

If you're still worried about this secret getting into the wrong hands, you can always store an encrypted version of the secret in your environment variable and use a library to decrypt this value when it is needed. This will render the secret almost useless, even if a bad actor has access to your environment. 

## Switching Environments

We usually want different values associated with different environments. This is usually solved with the use of environment variables. However, if you're like me, you may find that it would be a good idea to have a standard property file for local development with no dependency on the environment it is being run on. Spring makes this easy for us. 

Let us use our default `application.properties` for local development. We can configure this in plain text as we are only connecting to a local database with dummy data. 

```xml
spring.datasource.url=jdbc:mysql://localhost:3306/Project41
spring.datasource.username=project41
spring.datasource.password=SuperTopSecretPassword
```

We want a separate property file for our deployment which relies on environment variables. Let us define a new property file `application-deployment.properties`. 

```
spring.datasource.url=${DATASOURCE_URL}
spring.datasource.username=${DATASOURCE_USERNAME}
spring.datasource.password=${DATASOURCE_PASSWORD}
```

`application.properties` is our default property file and we do not need to do anything special to activate it. However, on our deployed environment, we can use the `SPRING_PROFILES_ACTIVE` environment variable set to `deployment` which tells Spring to use `application-deployment.properties` instead. No changes to the code or to the property files are needed, hence there is no need for separate branches for each environment! 

## Best Practices

Although environment variables are very useful for keeping our secrets safe and leaving our application easily configurable, there are some things to remember:

- **Regular Rotation of Secrets:** Remember to invalidate and rotate API keys, database passwords, and other sensitive data.
- **Use Property Encryption:** Encrypting secrets (wherever they live) is good practice.
- **Access Control:** Limit access to your environment. It would be pointless to store your secrets as environment variables if anyone can access your environment.
- **Validate External Inputs:** Make sure that your environment and environment variables are not susceptible to injection of any sort. For example, if you're using GitHub actions to deploy your environment, it is very easy to print the environment variables out to the logs given appropriate changes to your workflow!
