---
---
# Architecture Spring Security
### Security Filter Chain

In Spring Security, the security filter chain is a series of filters that intercept and process incoming HTTP requests to enforce security measures in a web application. The security filter chain is responsible for handling authentication, authorization, and other security-related tasks.

The security filter chain is comprised of a set of filter classes, each responsible for a specific security function such as authentication, authorization, CSRF protection, session management, and more. These filters work together in a specific order to apply the necessary security measures to incoming requests.

The order of filters in the security filter chain is important, as each filter depends on the output of the previous filter. The default security filter chain in Spring Security includes several filters such as the WebAsyncManagerIntegrationFilter, SecurityContextPersistenceFilter, HeaderWriterFilter, CsrfFilter, LogoutFilter, and UsernamePasswordAuthenticationFilter.

Developers can customize the default security filter chain or create their own by adding or removing filters or changing their order. This customization allows developers to tailor the security measures of the application to meet specific requirements.

Overall, the security filter chain is a crucial component of Spring Security that helps enforce security measures in web applications by processing incoming requests and applying appropriate security measures.

### Authentication Manager

In Spring Security, the default AuthenticationManager is an instance of ProviderManager, which is a composite implementation of the AuthenticationManager interface.

The ProviderManager delegates authentication to a list of AuthenticationProvider instances. When an Authentication object is passed to the authenticate method of the AuthenticationManager, the ProviderManager will iterate through its list of AuthenticationProvider instances until one of them is able to authenticate the user. If no AuthenticationProvider can authenticate the user, an exception will be thrown.

The default AuthenticationManager is created automatically by Spring Security and is typically used when no custom authentication provider or AuthenticationManager implementation is specified.

By default, the ProviderManager uses three built-in authentication providers:

DaoAuthenticationProvider: Authenticates users against a user database or other persistent storage.
AnonymousAuthenticationProvider: Provides anonymous authentication for unauthenticated users.
RememberMeAuthenticationProvider: Authenticates users based on a previously stored remember-me token.
Developers can customize the default AuthenticationManager by adding or removing authentication providers, or by creating their own custom authentication providers. This allows developers to implement custom authentication mechanisms or integrate with external authentication systems.

Overall, the default AuthenticationManager in Spring Security provides a flexible and extensible way to authenticate users using a variety of authentication providers.

