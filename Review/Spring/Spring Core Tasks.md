# 2-1 Use a Java Config to Configure POJOs

##### Problem

You want to manage POJOs with annotations with Spring's IoC container.

##### Solution

Design a POJO class. Next, create a Java config class with @Configuration and @Bean annotations to configure POJO instane values or set up Java components with @Component, @Repository, @Service, or @Controller annotations to later create POJO instance values. Next, instantiate the Spring IoC container to scan for Java classes with annotations. The POJO instance or bean instances then become accessible to put together as part of an application. 

##### @Configuration and @Bean

When we instantiate the Spring IoC container, Spring scan all Java classes that contain annotations. @Configuration denote a configuration class in Spring. When Spring encounters a class with @Configuration annotation, it looks for bean instance definitions in the class, which are Java methods decorated with the @Bean annotation. The Java methods create and return a bean instance. Any method definitions decorated with the @Bean annotation generates a bean name based on the method name. Alternatively, @Bean(name="myclass") add a new name to the bean instance.

Spring provides two type of IoC container implementations, *bean factory* and *application context*, which is the sub-interface of bean factory. So, in most applications, application context is common, and bean factory is only used for the case when the computation resource is limited (low end devices). 

