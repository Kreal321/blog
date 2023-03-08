---
title: Spring Security
tags:
  - Spring Boot
  - Spring Security
  - Filter
  - Jakarta EE
  - Servlet
---

## Servlet and Servlet Container

![](/blog/assets/images/spring-security/spring-servlet.png)

Servlets are a component of the Java EE framework used for web development. They are basically Java programs that run inside the boundaries of a container. On the whole, they are responsible for accepting a request, processing it, and sending a response back using the HTTP protocol. 

A servlet container, also known as a web container or a servlet engine, is a component of a web server or application server that manages the lifecycle of servlets. The servlet container is responsible for loading, initializing, and invoking servlets, as well as managing their threads and resources. It also provides the necessary infrastructure for servlets to communicate with clients using the HTTP protocol, such as managing cookies and handling sessions.

Apache Tomcat is a long-lived, open source Java servlet container that implements core Java enterprise (now Jakarta EE) specifications

## Dispatcher Servlet

### Dispatcher Servlet vs Servlet Container

The Dispatcher Servlet is a standard servlet that is responsible for dispatching requests to the appropriate handler servlet objects based on URL mapping. Its name comes from its role as a dispatcher. Although not a Spring-specific feature, the Spring Framework uses it extensively to implement its mechanisms.

Like any other servlet, the Dispatcher Servlet is deployed within a Servlet Container


## Filter

### What Is OncePerRequestFilter?

A filter can be executed before or after servlet processing, and if a request is forwarded to another servlet using the `RequestDispatcher`, it's possible for the same filter to be invoked multiple times. However, in certain scenarios, we may want to ensure that a specific filter is invoked only once per request. This is a common requirement when working with [Spring Security](/blog/spring-boot/spring-security), where certain authentication actions should only occur once per request.

To ensure a filter is only executed once per request, we can extend the `OncePerRequestFilter` provided by Spring. This abstract class guarantees that the filter's `doFilter()` method is executed only once per request, even if the filter is configured multiple times in the filter chain.

### Filter vs Interceptor

![](/blog/assets/images/spring-security/spring-filter-interceptor.jpeg)

Spring Interceptors are similar to Servlet Filters. An interceptor just allows custom pre-processing with the option of prohibiting the execution of the handler itself, and custom post-processing, having access to Spring Context. Interceptors will only execute after Filters.

??? info "Methods"

    - `preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)`: 
      This is used to perform operations before sending the request to the controller. This method should return true to return the response to the client.
    - `postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView)`: 
      This is used to perform operations before sending the response to the client.
    - `afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception exception)`: 
      This is used to perform operations after completing the request and response.

### WebFilter and ServletComponentScan

The `ServletComponentScan` annotation is necessary to enable scanning of Servlet components, including `@WebServlet`, `@WebFilter`, and `@WebListener` in a Spring Boot application and register them with the Servlet Container.

## Spring Security

### Configuration
#### 1. Component-based security configuration (Recommanded)

Spring framework encourage developers to move towards a component-based security configuration.

```java title="SecurityConfig.java"
@Configuration
public class SecurityConfiguration {

    @Bean
    public AuthenticationManager authenticationManagerBean(HttpSecurity http) throws Exception {
        // configure AuthenticationManager...
    }
         
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        // configure HTTP security...
    }
     
    @Bean
    public WebSecurityCustomizer webSecurityCustomizer() {
        // configure Web security...
    }
         
}
```

???+ example "Detailed Example"

    ```java title="SecurityConfig.java"
    @Configuration
    public class SecurityConfig {

        private UserService userService;
        private PasswordEncoder encoder;
        private JwtFilter jwtFilter;

        @Autowired
        public SecurityConfig(UserService userService, PasswordEncoder encoder, JwtFilter jwtFilter) {
            this.userService = userService;
            this.encoder = encoder;
            this.jwtFilter = jwtFilter;
        }

        @Bean
        public AuthenticationManager authenticationManagerBean(HttpSecurity http) throws Exception {
            AuthenticationManagerBuilder authenticationManagerBuilder = http.getSharedObject(AuthenticationManagerBuilder.class);
            authenticationManagerBuilder.userDetailsService(userService).passwordEncoder(encoder);
            return authenticationManagerBuilder.build();
        }

        @Bean
        public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
            http
                .csrf().disable()
                .addFilterAfter(jwtFilter, UsernamePasswordAuthenticationFilter.class)
                .authorizeRequests()
                .antMatchers("/api/login").permitAll()
                .antMatchers("/api/getAll", "/content/get/*").hasAuthority("read")
                .antMatchers("/api/create").hasAuthority("write")
                .antMatchers("/api/update").hasAuthority("update")
                .antMatchers("/api/delete/*").hasAuthority("delete")
                .anyRequest()
                .authenticated();

            return http.build();
        }

        @Bean
        public WebSecurityCustomizer webSecurityCustomizer() {
            return (web) -> web.ignoring().antMatchers("/images/**", "/js/**", "/webjars/**");
        }
    }
    ```

#### 2. Extended `WebSecurityConfigurerAdapter` class

Only if you are using Spring Security version 5.6.5 or older, or Spring Boot version 2.6.8 or older

!!! warning "The type `WebSecurityConfigurerAdapter` is deprecated"
    `WebSecurityConfigurerAdapter` class is deprecated after Spring Security 5.7.1 or Spring Boot 2.7.0, and the reason is that Spring framework encourage users to move towards a component-based security configuration. [Read More](https://spring.io/blog/2022/02/21/spring-security-without-the-websecurityconfigureradapter)

```java title="SecurityConfig.java"
@Configuration
@EnableWebSecurity
public class SecurityConfiguration extends WebSecurityConfigurerAdapter {

    @Override
    @Bean
    protected AuthenticationManager authenticationManager() throws Exception {
        return super.authenticationManager();
    }
 
    @Override
    protected void configure(HttpSecurity http) throws Exception {
         
        // configure HTTP security...
         
    }
 
    @Override
    public void configure(WebSecurity web) throws Exception {
         
        // configure Web security...
         
    }      
}
```

??? example "Detailed Example"

    ```java title="SecurityConfig.java"
    @Configuration
    public class SecurityConfig extends WebSecurityConfigurerAdapter {

        private UserService userService;
        private PasswordEncoder encoder;
        private JwtFilter jwtFilter;

        @Autowired
        public SecurityConfig(UserService userService, PasswordEncoder encoder, JwtFilter jwtFilter) {
            this.userService = userService;
            this.encoder = encoder;
            this.jwtFilter = jwtFilter;
        }

        @Bean
        public DaoAuthenticationProvider daoAuthenticationProvider(){
            DaoAuthenticationProvider provider = new DaoAuthenticationProvider();
            provider.setUserDetailsService(userService);
            provider.setPasswordEncoder(encoder);
            return provider;
        }

        @Override
        @Bean
        protected AuthenticationManager authenticationManager() throws Exception {
            return super.authenticationManager();
        }

        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http
                .csrf().disable()
                .addFilterAfter(jwtFilter, UsernamePasswordAuthenticationFilter.class)
                .authorizeRequests()
                .antMatchers("/api/login").permitAll()
                .antMatchers("/api/getAll", "/content/get/*").hasAuthority("read")
                .antMatchers("/api/create").hasAuthority("write")
                .antMatchers("/api/update").hasAuthority("update")
                .antMatchers("/api/delete/*").hasAuthority("delete")
                .anyRequest()
                .authenticated();
        }

        @Override
        public void configure(WebSecurity web) throws Exception {
            web.ignoring().antMatchers("/images/**", "/js/**", "/webjars/**");
        }
    }
    ```

