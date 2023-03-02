---

---
# Spring Security

## What is Spring Security
Spring Security is a framework dedicated to providing application security for Java applications in a flexible way. Spring Security addresses all the layers of security for your application. It is flexible, customizable and easy to use.

## Principles of Application Security

### Least Privilege

Principle of Least Privilege states that every user should only have just enough access to perform to perform their duties.

### Separation of Duties

The main idea behind Principle of Separation of Duties is that no single user or role should have too much authority. 

### Defense in Depth

It may be difficult to hack into a computer security system, but it never prevents a determined hacker from hacking into the system. So, always implement security in multiple layers and set up alerts for when the security system fails.

### Failing Securely

Principle of Failing Securely recognizes that all systems are bound to fail. This helps us to design systems that knows how to limit damage in case of any failures.

### Open Design

Principle of Open Design states that your system security should not rest on the secrecy of your implementation. This involves making the design process and the resulting application code accessible to a wider community, including other developers, security experts, and end-users. Develop your app in such a way that a hacker will not be able to exploit your app even if they gain access to the source code.

### Avoiding Security by Obscurity

Principle of Avoiding Security by Obscurity suggests that relying solely on the secrecy or obscurity of the credentials to provide security is not a reliable or effective approach. This means that security measures should not rely on the assumption that an attacker will not be able to discover the underlying details of a system or its components like a privileged username and password.

### Reduce Your Attack Surface

When designing an application, your goal should be to minimize the number of entry points for attackers.

## Key concepts in Application Security

### Authentication 
Authentication is the process of verifying that an individual, entity or website is whom it claims to be, by using a proof of identity. The proof of identity can be knowledge-based like ID and password, PIN number etc. It can also be possession-based like phone call/text message verification, key card/badges, access token device etc.

Now-a-days most applications and services offer multi-factor authentication, a combination of knowledge-based and possession-based authentication.

![Authentication](images/AuthConfigFlow.png)

### Authorization 
Authorization may be defined as the process of verifying that a requested action or service is approved for a specific/principal. It is the second stage of access control, following authentication, which verifies the identity of the user or entity requesting access.

## Introduction to Spring Security

![SpringWithSecurity](images/SpringMVCFlowWSecurity.png)

Spring Security works by providing a set of security filters that are applied to incoming requests to your application. These filters intercept the requests and perform various security checks and operations, such as verifying the user's identity, checking their permissions and roles, and managing user sessions.

Here's a high-level overview of how Spring Security works:

1. Intercepting incoming requests: When a request is made to your application, it is intercepted by a set of Spring Security filters.

2. Authentication: The first step in the security process is authentication, which verifies the user's identity by checking their credentials against a stored database or external authentication provider.

3. Authorization: Once the user has been authenticated, Spring Security checks their authorization to access the requested resource. Authorization is based on access control policies and rules that determine which users are allowed to access which resources.

4. Session Management: Spring Security also manages user sessions, which enable users to stay logged in to your application for a period of time. It provides a set of configurable session management features such as session timeout, session fixation prevention, and concurrent session control.

The following is a simplified view of Spring Security work flow:

![Flow](images/SpringSecurityFlow.png)

## How to use Spring Security

### Add Spring Security Dependency

In order to start using Spring Security, all you have to do is add the Spring Security dependency to your Spring Boot application. 

In Spring boot maven application add the following dependency to your pom.xml:
```
    <dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-security</artifactId>
	</dependency>
```
If you are using Spring Security without Spring Boot, add the following dependency to your pom.xml:
```
    <dependency>
		<groupId>org.springframework.security</groupId>
		<artifactId>spring-security-web</artifactId>
        <version>VERSION</version>
	</dependency>
	<dependency>
		<groupId>org.springframework.security</groupId>
		<artifactId>spring-security-config</artifactId>
        <version>VERSION</version>
	</dependency>
```

Simply adding the dependency provides following security features and more to your application by default:

1. Form-based authentication for all URLs.
2. Single user with username = *user* and a autogenerated random password. 
3. Manages user sessions by default, with options to configure session fixation, session concurrency, and logout options.
4. Default URL patterns for authentication and authorization. For example, "/login" is the default URL for the login page, and "/logout" is the default URL for logging out.
5. Adds a login form with fields username and password.
6. Handles login error.

The default user credentials generated by Spring Security can be overridden by adding the properties to `application.properties` file.

```
    spring.security.user.name=foo
    spring.security.user.password=bar
```


###  Configuring Spring Security

Create a security configuration class and annotate it with *@EnableWebSecurity* and *@Configuration* annotations. Implement the *WebSecurityConfigurer* interface, which provides methods to configure security settings.

```

```

```java
public class Tutorial {
    public static void main(String...args){
        
    }
}

```


