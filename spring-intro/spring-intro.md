# Introduction to Spring

## Tight Coupling

Tight coupling in software modules means they are highly dependent on each other, with changes in one module potentially requiring modifications in multiple other modules. This can make the system less flexible, harder to maintain, and hinder scalability and reusability.

## Loose Coupling

Loose coupling in software modules means they are relatively independent and have minimal dependencies on each other. They communicate through well-defined interfaces, which allows for flexibility, easier maintenance, and promotes scalability and reusability in the software system.

## Inversion of Control

Inversion of Control is a principle in Software Engineering that transfer control of objects or portion of code to a framework or container.

Spring IoC(Inversion of Control) Container is the core of Spring Framework. It takes control of the program by creating objects, managing dependencies and lifecycles.
In traditional programming, our custom code makes calls to libraries to implement features and our code controls the flow of the program. But with IoC, frameworks or containers call our custom code and control the flow of the program.

## Dependency Injection

Dependency Injection is a design pattern in Software Engineering used to implement IoC. It transfers the responsibility of creating objects to Spring Framework. DI makes the code more modular, testable, and maintainable by reducing coupling between classes and enabling easier unit testing. `@Autowired` annotation is used to iject dependency in spring.

There are three types of Dependency Injection:
* Constructor Injection:  The container provides the dependencies by invoking a constructor with the necessary arguments.
* Setter Injection: The container will use setter methods of the class after invoking a no argument constructor, to instantiate the class.
* Field Injection: The dependencies of a class are injected into its fields rather than its constructor or setter methods.

**@Qualifier**: Used to specify which bean should be injected when there are multiple beans of the same type available.

## Configuring Spring Application
Spring applications can be configured using XML files, Java-based configuration, or a combination of both.

### XML-based
XML-based configuration involves defining beans, dependencies, and their properties in an XML file.
An XML-based configuration file would look like the following:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- bean definitions here -->
    <bean id="..." class="..."> </bean>

</beans>
```

### Java-based
Java-based configuration uses Java classes to define beans and their dependencies.

This approach has several benefits, including:

* Type safety: Java-based configuration uses Java classes, which are strongly typed, making it less error-prone than XML-based configuration.

* Ease of refactoring: As Java-based configuration is based on classes, it is easier to refactor code without worrying about updating XML files.

* Better IDE support: IDEs such as Eclipse and IntelliJ IDEA provide better support for Java code than XML files.

To configure a Spring application using Java-based configuration, create a class annotated with the `@Configuration` annotation. This class will contain one or more methods annotated with the `@Bean` annotation, which will define the beans that make up the application.

**@Configuration**: The @Configuration annotation in Spring is used to mark a Java class as a configuration source for defining and configuring beans in a Spring application. It is used in conjunction with other annotations, such as @Bean, to define bean definitions, specify scopes, and control bean initialization and destruction.

**@Bean**: A bean in Spring is any java object that is created, configured, and managed by the Spring container.

**@Component**: Used to mark a class as a Spring-managed component, making it eligible for automatic detection and instantiation as a bean during the component scanning process

**@ComponentScan**: Used to specify the packages that should be scanned for Spring-managed components during the component scanning process. It is typically used in conjunction with @Configuration to enable component scanning in a Spring application. 

### Configuration Spring Expression Language (SpEL)
Spring Expression Language, or SpEL for short, is a powerful expression language that is used in Spring applications for configuring and manipulating objects. It provides a way to dynamically evaluate and manipulate expressions at runtime, which can be useful in a variety of contexts, such as configuration files, annotations, and data binding.

SpEL supports a wide range of features, including:

-  **Property access**: SpEL allows you to access object properties using a syntax similar to that of Java. For example, suppose you have a Java object called "person" with two properties: "firstName" and "lastName". You can access these properties in SpEL using the following syntax:
```bash 
#{person.firstName}
#{person.lastName}
```
In this example, the `#` character indicates that this is an expression that should be evaluated at runtime, and the `.` character is used to access the object properties.

-  **Method invocation**: SpEL allows you to invoke methods on objects using a syntax similar to that of Java. For example, suppose you have a Java object called "calculator" with a method called "add" that takes two parameters. You can invoke this method in SpEL using the following syntax:
```bash
#{calculator.add(2, 3)}
```
In this example, the `()` characters are used to indicate that this is a method invocation, and the parameters are passed inside the parentheses

-  **Conditional expressions**: SpEL allows you to use conditional expressions to perform conditional logic, such as if-else statements. For example, suppose you have a Java object called "person" with a property called "age". You can use a conditional expression in SpEL to check if the person is over 18 years old:
```bash
#{person.age >= 18 ? 'Adult' : 'Minor'}
```
In this example, the `?` and `:` characters are used to indicate the if-else logic. If the person's age is greater than or equal to 18, the expression will evaluate to "Adult". Otherwise, it will evaluate to "Minor".

-  **Mathematical and logical operators**: SpEL supports a wide range of mathematical and logical operators, such as +, -, *, /, %, &&, ||, and !. For example, you can perform basic arithmetic operations in SpEL using the following syntax:
```bash
#{2 + 3}
#{10 - 5}
#{2 * 4}
#{10 / 2}
```

-  **Regular expressions**: SpEL supports regular expressions, which can be used for pattern matching and data validation. For example, you can use a regular expression in SpEL to validate that an email address is in the correct format: 
```bash
#{email.matches('[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}')}
```
In this example, the `matches` method is used to check if the email address matches the specified regular expression.

## Bean Life Cycle

In Spring, a bean's lifecycle consists of several stages, each with its own set of methods that can be executed. The following is a general overview of the bean lifecycle stages and the corresponding methods:

![Bean Life Cycle](images/BeanLifeCycle.png)

1. Bean instantiation: This is the first stage of the bean lifecycle.bThe container creates an instance of the bean using its constructor or a factory method, depending on how the bean is defined.

2. Dependency injection: The container injects any required dependencies into the bean instance.

3. Initialization: The init method is a callback method that you can define for a bean to perform any custom initialization logic. This method is executed after the bean has been instantiated and all its dependencies have been injected, but before the bean is ready to be used.
To define an init method for a bean, you can use the `@PostConstruct` annotation on a method in the bean class.

4. Destruction: This stage occurs when the bean is no longer needed, and the container wants to dispose of the bean. The following methods are executed during this stage:
    
    - *DisposableBean.destroy()*: This method is called before the bean is destroyed, giving it an opportunity to release any resources it is holding.
    
    - Custom destroy method: You can define a custom destroy method by specifying a method name in the bean configuration.

**@PostConstruct**: Indicates that a method should be executed after a bean has been constructed and its dependencies have been injected, but before the bean is put into service.

**@PreDestroy**: Indicates that a method should be executed before a bean is destroyed or removed from service.
