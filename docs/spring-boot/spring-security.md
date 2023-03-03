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