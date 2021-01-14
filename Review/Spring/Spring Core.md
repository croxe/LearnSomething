# core Technologies 

Spring Framework's Inversion of Control (IoC) container covers 80% Aspect-Oriented Programming (AOP) requirements. 

AspectJ - the most mature AOP implement in the Java enterprise space.

### The IoC container 

IoC is also known as Dependency injection (DI). It is a process that objects define by their dependencies, which similar to a factory method. The container injects those dependencies when it creates the bean. The bean can control the instantiation or location of its dependencies by using direct construction of classes, or a mechanism such as the service Locator pattern. 

org.springframwork.beans and org.springframework.context packages are the basis for Spring Framework's IoC container. The BeanFactory interface provides an advanced configuration mechanism capable of managing any type of object (for enterprise). ApplicationContext is a sub-interface of BeanFactory. It adds easier integration with Spring's AOP features; message resource WebApplicationContext for use in web applications.

