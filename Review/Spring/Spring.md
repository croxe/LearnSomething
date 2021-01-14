# Spring Framework

### Dependency Lookup

The Dependency Lookup is an approach where we get the resource after demand.

We could get resource by directly new keyword;

```java
A obj = new AIiml();
```

Or, by static factory method;

```java
A obj = A.getA();
```

Or, get resource from JNDI(Java Naming Directory Interface).

```java
Context ctx = new InitialContext();
Context environmentCtx = (Context) ctx.lookup("java:comp/env");
A obj = (A) environmentCtx.lookup("A");
```

### Dependency Injection 

Dependency Injection is a design pattern that removes the dependency from the programming code so that it can be easy to manage and test the application. In this case, we provide external source, like XML files, to provide information for objects. Therefore, we need MVC-pattern that define model, which is the skeleton object. Meanwhile, the controller is the loading module that inject the source information to the object models. 


### Dependency Injection by Constructor

In XML, the <constructor-arg> is the subelement of <bean>. 

We can inject:
1. Primitive and String-based value
2. Dependent object (might also contain objects)
3. Collection values 

The default getting parameter from XML is **String Type**, if we don't specify the type of a value in XML then it will be a string.


### Spring AOP 

Aspect Oriented Programming (AOP) compliments OOPs, rather focus on class, it focuses on the key unit of modularity.
AOP breaks the program logic into distant parts (called concerns). It is used to increase modularity by cross-cutting concerns. 
A cross-cutting concern is a concern that can affect the whole application and should be centralized in one location in code as possible, such as transaction management, authentication, logging, security etc.

##### Why use AOP?

It provides the pluggable way to dynamically add the additional concern before, after or around the actual logic. Suppose there are 10 methods in a class as given below:

> class A{  
public void m1(){...}  
public void m2(){...}  
public void m3(){...}  
public void m4(){...}  
public void m5(){...}  
public void n1(){...}  
public void n2(){...}  
public void p1(){...}  
public void p2(){...}  
public void p3(){...}  
}  

## *Need better interpretation* 

**Problem Rise**: If I have to maintain log and send notification after calling methods that starts from m. 

**Problem without AOP**: We can call methods (that maintains log and sends notification) from the methods starting with m. In such scenario, we need to write the code in all the 5 methods. But, if client says in future, we don't have to send notification, and we need to change all the methods. Which leads to the maintenance problem. 

**Solution with AOP**: We don't have to call methods from the method m. Now we can define the additional concern like maintaining log, sending notification etc. In the method of a class. Its entry is given in the xml file. 
In future, if client says to remove the notifier functionality, we need to change only in the xml file. So, maintenance is easy in AOP. 


##### Where use AOP?

AOP is mostly used in following cases:

- to provide declarative enterprise services such as declarative transaction management.
- It allows users to implement custom aspects.

### AOP Concepts and Terminology

**Join point**

Join point is any point in your program such as method execution, exception handling, field access, etc. Spring supports only method execution join point. 

**Advice**

Advice represents an action taken by an aspect at a particular join point. There are different types of advices:

- **Before Advice**: It executes before a join point.
- **After Returning Advice**: It executes after a join point completes normally.
- **After Throwing Advice**: It executes if method exits by throwing an exception.
- **After (finally) Advice**: It executes after a join point regardless of join point exit whether normally or exceptional return.
- **Around Advice**: It executes before and after a join point. 

**Pointcut**

??? (What is that ?) It is an expression language of AOP that matches join points. 

**Introduction**

It means introduction of additional method and field for a type. It allows you to introduce new interface to any advised object.

**Aspect**

It is a class that contains advices, joinpoints, etc.

**Interceptor**

It is an aspect that contains only one advice.

**AOP Proxy**

It is used to implement aspect contracts, created by AOP framework. It will be a JDK dynamic proxy or CGLIB proxy in spring framework.

**Weaving**

It is the process of linking aspect with other application types or objects to create an advised object. Weaving can be done at compile time, load time or runtime. Spring AOP performs weaving at runtime. 



