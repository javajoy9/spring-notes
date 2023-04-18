# Introduction to Spring Boot

## Spring vs Spring Boot

Spring Boot is built on top of Spring and includes many of the same features, but with additional conventions and defaults to simplify development. Spring and Spring Boot can be used together or independently, depending on the requirements and preferences of the development team.
 
### Spring

* Comprehensive Java framework for building enterprise applications.
* Provides a wide range of features, including dependency injection, aspect-oriented programming, data access, security, and more.
* Follows a modular approach, allowing developers to choose the modules they need and use them as needed.
* Highly extensible and customizable, with a large ecosystem of modules and integrations.
* Provides flexibility and freedom in application architecture and configuration.

### Spring Boot

* Sub-project of Spring that provides a streamlined and opinionated way of building Java applications.
* Simplifies configuration and setup with default configurations and conventions.
* Focuses on simplicity and ease of use, particularly for building microservices and containerized applications.
* Includes an embedded web server, eliminating the need for external web servers.
* Includes pre-configured templates for common tasks, such as data access, security, and more.
* Designed for modern, cloud-native applications with features like health checks, metrics, and monitoring.

## Spring Boot Auto Configuration

Spring Boot's auto-configuration feature allows developers to easily configure their applications without having to write a lot of boilerplate code. It automatically configures many of the commonly used components, such as data sources, security, and web frameworks. Spring Boot auto-configuration works by scanning the classpath for certain libraries and components, and configuring the application based on what it finds. For example, if the classpath contains a database driver, Spring Boot will automatically configure a DataSource bean.

Auto-configuration can also be customized and extended by providing custom configuration classes. These classes can be annotated with `@Configuration` and can contain `@Bean` methods that override or augment the auto-configured beans. You need to opt-in to auto-configuration by adding the `@EnableAutoConfiguration` or `@SpringBootApplication` annotations to one of your `@Configuration` classes.

## Conditional Matching

Conditional matching is a feature in Spring Boot that allows developers to selectively enable or disable certain configurations or beans based on specific conditions. This is often used to dynamically configure the behavior of an application based on runtime conditions or external configuration.

In Spring Boot, conditional matching is achieved using the `@Conditional` annotation, which can be applied to configuration classes or bean methods. The `@Conditional` annotation takes one or more conditions as parameters, and the annotated configuration class or bean method will only be processed or created if the specified conditions are met.

### Profiles
Profiles in Spring Boot provide a way to define different sets of configurations for different environments or deployment scenarios. With profiles, you can configure your application to behave differently depending on the environment it is running in, such as development, testing, staging, or production.

To define a profile in Spring Boot, you can use the `@Profile` annotation. This annotation can be added to any bean definition, indicating that the bean should only be created when the specified profile is active. For example, suppose you have a bean called "myService" that should only be created when the "dev" profile is active. You can define the bean as follows:
```java
@Service
@Profile("dev")
public class MyService {
  // ...
}
```

In this example, the `@Service` annotation indicates that this is a service bean, and the `@Profile("dev")` annotation indicates that the bean should only be created when the "dev" profile is active.

To activate a profile in Spring Boot, you can use the spring.profiles.active property. This property can be set in a variety of ways, such as through a configuration file, a system property, or an environment variable. For example, to activate the "dev" profile, you can set the spring.profiles.active property in your application.properties file as follows:
```
spring.profiles.active=dev
```

## Core Annotations

Spring Boot is built on top of the Spring framework and provides a number of core annotations that are commonly used in Spring Boot applications. These annotations are used to configure various aspects of the application, such as defining beans, handling properties, enabling specific features, and more. Here are some core annotations in Spring Boot:

* **@SpringBootApplication**: This annotation is the starting point of a Spring Boot application. It is a combination of multiple annotations, including @Configuration, @EnableAutoConfiguration, and @ComponentScan, and is used to configure and bootstrap a Spring Boot application. It is typically applied to the main class of the application.

* **@Configuration**: This annotation indicates that a class contains configuration methods that define beans. Beans are objects managed by the Spring container, and configuration methods annotated with @Configuration are used to define and configure these beans.

* **@EnableAutoConfiguration**: This annotation enables Spring Boot's auto-configuration feature, which automatically configures various components and settings based on the classpath and application's dependencies. It helps in reducing the amount of boilerplate configuration code that needs to be written in a Spring Boot application.

* **@ComponentScan**: This annotation enables the scanning of components (such as beans, controllers, services, etc.) in specified packages or base packages. It allows Spring to automatically discover and register components in the application context, making them available for dependency injection and other Spring features.

* **@Value**: This annotation is used to inject values from external properties files, environment variables, or other sources into Spring beans. It allows developers to externalize configuration and manage application properties without hardcoding them in the code.

* **@Profile**: This annotation is used to define profiles for different environments (such as development, production, etc.) in a Spring Boot application. Beans or configurations annotated with @Profile will be activated or deactivated based on the active profiles, allowing for different behavior in different environments.

* **@Conditional**: This annotation is used to selectively enable or disable configurations or beans based on specific conditions, as discussed in the previous answer. It allows for dynamic configuration of the application based on runtime conditions or external configuration.

## Aspect Oriented Programming

Aspect-Oriented Programming(AOP) is a programming paradigm that allows you to modularize cross-cutting concerns in your application. In Spring, AOP is implemented using AspectJ, which provides a powerful set of tools for defining and applying aspects to your application.

One of the key concepts in AOP is the notion of a pointcut, which is a set of joinpoints where you can apply an aspect. A joinpoint is a specific point in the execution of your application, such as a method invocation or a field access. By defining a pointcut, you can specify the set of joinpoints where you want to apply an aspect.

In Spring, you can define a pointcut using a combination of a pointcut expression and a pointcut designator. The pointcut expression is a SpEL expression that specifies the joinpoints that match the pointcut, and the pointcut designator specifies the types of joinpoints that the pointcut applies to.

For example, suppose you have a `MyService` class that contains several methods, and you want to log the entry and exit of each method. You can define a pointcut that matches all public methods of the `MyService` class, like this:
```java
@Pointcut("execution(public * com.example.MyService.*(..))")
public void myServiceMethods() {}
```

In this example, the `@Pointcut` annotation is used to define a pointcut called `myServiceMethods`. The SpEL expression `execution(public * com.example.MyService.*(..))` specifies that the pointcut applies to all public methods of the `MyService` class.

Once you have defined a pointcut, you can apply an aspect to it using an advice. An advice is a piece of code that is executed at a specific joinpoint, such as before or after a method invocation. In Spring, you can define an advice using an aspect, which is a class that contains one or more advice methods.

For example, suppose you have a `LoggingAspect` class that contains advice methods for logging the entry and exit of methods. You can apply the `LoggingAspect` to the `myServiceMethods` pointcut, like this:
```java
@Aspect
@Component
public class LoggingAspect {
    @Before("myServiceMethods()")
    public void logMethodEntry(JoinPoint joinPoint) {
        String methodName = joinPoint.getSignature().getName();
        System.out.println("Entering " + methodName);
    }

    @After("myServiceMethods()")
    public void logMethodExit(JoinPoint joinPoint) {
        String methodName = joinPoint.getSignature().getName();
        System.out.println("Exiting " + methodName);
    }
}
```

In this example, the `@Aspect` annotation is used to define the LoggingAspect as an aspect. The `@Before` and `@After` annotations are used to define advice methods that are executed before and after a method invocation, respectively. The `myServiceMethods()` pointcut is used to specify the joinpoints where the aspect should be applied.

