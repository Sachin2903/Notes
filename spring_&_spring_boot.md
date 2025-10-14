# Spring & spring boot

>> spring is a lightweight and popular open source java based frameworks

##### feature of spring framework 
1. Inversion fo control (IOC)
the IOC container manages the lifecyclel and configuration of application object (beans) , making it easiter to manage dependecies and object creation

we can define the beans and their dependencies in a configuration file and the IOC contaner handles the instantiation of these beans

2. Dependency Injection
DI is a way to inject the dependencies rather then having to create or manage them expicitly. It is achived through spring IOC contianer which is responisble for creating and managing object known as beans

###### types fo dependenct injection in spring

1. contructor injection 
```java
@Autowired
private Car(Engine engine){
    this,engine =engine
}
```

2. Setter Injection
```java
public class Car{
    private Engine engine;

    @Autowired
    public void setEngine(Engine engine){
        this.engine=engine;
    }
}
```

3. Field Injection
```java
private Engine engine;
```


3. Aspect -Oriented Programing (AOP)
AOP helps separate cross cutting concerns from business logic . it allows you to add additional behaviour to code without modifying the code itself

4. Spring MVC
A framework for building web applications, SPring MVC follows the Model-VIew-COntroller (MVC) desing pattern. It simplifies the development of web application by providing an efficinet way to handle HTTP request and response

5. Transation Management
make earier in databse transaaction by using spring transaction management abstraction 

6. spring secuirty
A custom authentication and authorization framework

7. Spring Boot
ALthrough a part of the broader sping ecosystem, spring boot is a tool that simplifies the development of new spring applications. It comes with embedded servers, auto-configuration and production ready features such as metrics and health checks

##### Spring vs Spring boot
jdk
intejj
maven