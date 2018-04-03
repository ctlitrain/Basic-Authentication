# Basic authentication

We will be creating a spring boot application with Basic Authenication using Spring security.

## What is API Security?

API Security is a wide area with many different definitions, meanings, and solutions. The main key terms in API security are Authorization, Authentication.

## What is Authentication?

Authentication is used to reliably determine the identity of an end user and give access to the resources based on the correctly identified user.

## What is Authorization?

Authorization is the process of giving an entity permission to do, use, or obtain something.

## What is Basic Authentication?

Basic Authentication is the simplest way to enforce access controling to resources. Here, the HTTP user agent provides the username and the password when making a request. The string containing the username and password separated by a colon is Base64 encoded before sending to the backend when authentication is required.

### Steps:

1) Go to  start.spring.io and select the below dependencies:

```
1) spring-boot-starter-actuator
2) spring-boot-starter-security
3) spring-boot-starter-web

```
2) Configuration class is annotated with @EnableWebSecurity annotation and configuration class is extended from the WebSecurityConfigurerAdapter. The EnableWebSecurity annotation will enable Spring-Security web security support.

```
@EnableWebSecurity
@Configuration
public class SecuityConfig extends WebSecurityConfigurerAdapter {
```
3) Overridden configure(HttpSecurity) method is used to define which URL paths should be secured and which should not be. In my example  only admin can access all the endpoints with basic auth.

```
httpSecurity.authorizeRequests()
                .anyRequest().access("hasRole('ADMIN')")
```

4) In the configure(AuthenticationManagerBuilder) method, I have created an in-memory user store with a users. There I have added username, password, and userole for the in-memory user.

```
authenticationManagerBuilder.inMemoryAuthentication()
                .withUser("rahul").password("test").roles("ADMIN")
                .and().withUser("kumar").password("test1").roles("USER");
```

## Steps to build and run the application:

1) git clone https://github.com/ctlitrain/Basic-Authentication.git
2) mvn clean
3) mvn spring-boot:run

## Results:

1) If you hit the endpoint [localhost:8088/rest/hello](http://localhost:8088/rest/hello) with username=kumar and password=test1, you will get unauthorized 401 error as he is not an admin.

2) If you login with username=rahul and password=test, you will get the "Hello World" as he is the admin.
