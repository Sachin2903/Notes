# Spring & spring boot

>> spring is a lightweight and popular open source java based frameworks , was developed in 2003

#### feature of spring framework 
1. Inversion fo control (IOC)
the IOC container manages the lifecyclel and configuration of application object (beans) , making it easiter to manage dependecies and object creation

we can define the beans and their dependencies in a configuration file and the IOC contaner handles the instantiation of these beans

2. Dependency Injection
DI is a way to inject the dependencies rather then having to create or manage them expicitly. It is achived through spring IOC contianer- which is responisble for creating and managing object known as beans

* IOC is responsibl e for creatign and managing beans.
* DI is responisble for injecting the created beans into other beans where they are needed.

#### types fo dependenct injection in spring

1. contructor injection 
```java
@Autowired
private Car(Engine engine){
    this.engine =engine
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
@Autowired 
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
ALthrough a part of the broader spring ecosystem, spring boot is a tool that simplifies the development of new spring applications.  

##### Spring boot setup
jdk --> sudo apt install openjdk-21-jdk -y
intejj  sudo snap install intellij-idea-community --classic
maven sudo apt install maven -y
github repo 

spring boot intializer
###### Spring Web
Builds REST APIs and web applications using Spring MVC (controllers, routing, JSON handling).

###### Spring Data JPA
Simplifies database access using JPA/Hibernate—write less SQL, more repository interfaces.

###### H2 Database
Lightweight in-memory database mainly used for development and testing.

###### Spring Boot DevTools
Improves developer experience with auto-restart, live reload, and faster development.

###### Lombok
Reduces boilerplate code by auto-generating getters, setters, constructors, etc.

###### Maven clean install
--> this do clean install
mvn clean install

--> this skip tests and do clean install
mvn clean install -DskipTests

src -> main -> java -> com.test.springboot-> SpringbootApplication.java

#### Annotations
@Component , @Bean , @Configuration , @Controller , @RestController , @Service , @Repository

public → everyone
protected → family + neighbors
default → neighbors only
private → only me

###### @Component
Marks a class as a Spring-managed bean  
,Enables dependency injection and lifecycle management  

when main class run it find the class --> create the object --> handle dependencies --> inject the bean to all class where ever it needed

```java
@Component
public class EmailUtil {}

can use @Component class in these way
MyClass myclass = new MyClass()
or 
ApplicationContext context=SpringApplication.run(DemoApplication.class, args);
MyClass myclass =context.getBean(MyClass.class);
```

```java
private MyClass myClass;
public MyApp(MyClass myClass){
this.myClass=myClass
}

or 
use @Autowired()
priate MyClass myClass;
but class must be @Component
```

default value
public MyComponent(@Value("10") int a)

###### @AutoWired
use when inject class. class must be @Component or @Bean and @Conifguration

###### @Bean

Category: Bean definition method
What: Registers the return object as a Spring bean
Why: Full control over object creation
When to Use: External libraries, custom initialization

```java
@Bean
public PasswordEncoder passwordEncoder() {
    return new BCryptPasswordEncoder();
}

@Configuration
public class MyAppConfig{

 @Bean
 public MyComponent myComponent(){
    return new MyCompoennt();
 }
}
```

###### @Configuration

Category: Configuration
What: Marks a class as a source of bean definitions
Why: Java-based configuration (replaces XML)
When to Use: Application setup, third-party library config

```java
@Configuration
public class AppConfig {}
```


###### @Service

Category: Business layer stereotype
What: Specialized @Component for business logic
Why: Better readability, supports transactions
When to Use: Business rules, validations, workflows

```java
@Service
public class UserService {}
```

###### @Repository

Category: Persistence layer stereotype
What: Specialized @Component for data access
Why: Translates database exceptions into Spring exceptions
When to Use: DAO classes, database operations

```java
@Repository
public class UserRepository {}
```

Note:
If you extend JpaRepository, CrudRepository, or MongoRepository, this annotation is optional.

###### @Controller

Category: Web (MVC) layer
What: Handles HTTP requests for MVC applications
Why: Separates request handling and view rendering
Returns: View names (HTML, JSP, Thymeleaf)
When to Use: Server-side rendered web apps

```java
@Controller
public class PageController {

    @GetMapping("/home")
    public String home() {
        return "home";
    }
}
return html & template
```

###### @RestController

Category: Web (REST) layer
What: Controller for REST APIs
Equivalent To: @Controller + @ResponseBody
Why: Automatically converts response to JSON/XML
When to Use: Backend APIs for frontend/mobile apps

```java
@RestController
public class UserController {

    @GetMapping("/users")
    public List<User> users() {
        return List.of();
    }
}
return json
```

How Spring Detects These Annotations
1. Spring scans packages under @SpringBootApplicatio
2. All stereotypes are auto-detected via component scannin
3. Keep classes in the same or sub-packages

##### Lombok Annotations


✅ Overall: Lombok makes Spring Boot code cleaner, shorter, and easier to maintain.

# 🚀 Lombok Annotations – Practical Examples (Single File)

> Lombok reduces boilerplate code like getters, setters, constructors, and loggers — making Java cleaner and easier to read.

---

# ✅ 1. @Getter and @Setter
Automatically generates getter and setter methods for fields.

## Example: Bank Account

```java
import lombok.Getter;
import lombok.Setter;

@Getter
@Setter
class BankAccount {

    private String accountHolder;
    private double balance;
}

// Usage
public class Main {
    public static void main(String[] args) {

        BankAccount acc = new BankAccount();
        acc.setAccountHolder("Sachin");
        acc.setBalance(5000);

        System.out.println(acc.getAccountHolder());
        System.out.println(acc.getBalance());
    }
}
```

👉 **Why use it?**  
✔ Eliminates repetitive getter/setter code  
✔ Keeps classes clean  

---

# ✅ 2. @NoArgsConstructor
Creates a constructor with **no parameters**.

## Example: Required by Hibernate / JPA

```java
import lombok.NoArgsConstructor;

@NoArgsConstructor
class Customer {

    private String name;
}
```

Equivalent to:

```java
public Customer() {}
```

👉 **Why important?**  
Many frameworks (**Spring, Hibernate**) require a default constructor.

---

# ✅ 3. @AllArgsConstructor
Creates a constructor including **every field**.

## Example: Quick Object Creation

```java
import lombok.AllArgsConstructor;

@AllArgsConstructor
class Laptop {

    private String brand;
    private int ram;
}
```

### Usage:

```java
Laptop laptop = new Laptop("Apple", 16);
```

👉 Perfect when you want fast object initialization.

---

# ✅ 4. @Data (Most Popular)
A shortcut annotation that bundles:

✔ Getter  
✔ Setter  
✔ toString()  
✔ equals()  
✔ hashCode()  
✔ Required constructor  

## Example: DTO (Data Transfer Object)

```java
import lombok.Data;

@Data
class UserDTO {

    private String username;
    private String email;
}
```

### Usage:

```java
UserDTO user = new UserDTO();
user.setUsername("sachin123");
user.setEmail("sachin@gmail.com");

System.out.println(user);
```

Output:

```
UserDTO(username=sachin123, email=sachin@gmail.com)
```

👉 **Best used for:**  
✅ DTOs  
✅ Request/Response models  

⚠️ **Avoid on JPA Entities** — can cause performance issues due to `equals()` and `hashCode()`.

---

# ✅ 5. @ToString
Generates a readable string representation of an object.

## Example:

```java
import lombok.ToString;

@ToString
class Book {

    private String title;
    private double price;
}
```

### Usage:

```java
Book b = new Book();
System.out.println(b);
```

Output:

```
Book(title=null, price=0.0)
```

👉 Great for debugging.

---

# ✅ 6. @Slf4j (Logger Made Easy)
Automatically creates a logger named `log`.

## Example: Service Class

```java
import lombok.extern.slf4j.Slf4j;

@Slf4j
class PaymentService {

    public void processPayment() {

        log.info("Payment started");

        try {
            int result = 10 / 2;
            log.debug("Calculation successful: {}", result);

        } catch (Exception e) {
            log.error("Payment failed", e);
        }

        log.info("Payment completed");
    }
}
```

👉 Without Lombok you'd write:

```java
private static final Logger log =
LoggerFactory.getLogger(PaymentService.class);
```

✔ Saves time  
✔ Cleaner code  

---

# ✅ 7. @Builder ⭐ (Senior Developer Favorite)

Used when a class has many fields and constructors become confusing.

## Problem WITHOUT Builder:

```java
Student s = new Student("Sachin", 25, "Delhi", "India", "Male");
```

❌ Hard to remember order  
❌ Easy to make mistakes  

---

## Solution WITH Builder:

```java
import lombok.Builder;

@Builder
class Student {

    private String name;
    private int age;
    private String city;
    private String country;
}
```

### Usage:

```java
Student s = Student.builder()
        .name("Sachin")
        .age(25)
        .city("Delhi")
        .country("India")
        .build();
```

👉 Much more readable ✔  
👉 No order confusion ✔  
👉 Immutable-friendly ✔  

---

### REST API
1:22min

```java
import jakarta.persistence.*;
import lombok.*;

@Entity
@Getter
@Setter
@NoArgsConstructor
@Table(name="priduct")
@EqualsAndHashCode(onlyExplicitlyIncluded = true)
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @EqualsAndHashCode.Include
    private Long id;

    private String name;
    private String email;
}
```
generatedTYpe strategy
IDENTITY → DB makes auto-increment ID (mostly MySQL)
SEQUENCE → uses database sequence (PostgreSQL/Oracle)
AUTO → JPA selects best strategy automatically
TABLE → uses a separate table to generate I@OneToOne(fetch = FetchType.LAZY)Ds (slower, rarely used)
UUID → generates random unique ID (good for microservices/distributed systems)

##### relation ships in enitities
1. OneToOne
```java
User{
    @Id
    private int id;

    @OneToOne(
    cascade = CascadeType.ALL,
    fetch = FetchType.LAZY,
    optional = false,
    )
     @JoinColumn(
    name = "profile_id",
    referencedColumnName = "id",
    nullable = false,
    unique = true
    )
    private Profile profile;
}

Profile{
    @Id
    private int id;

    @OneToOne(mappedby='profile')
    private User user;
} 

@JoinColumn is owner

🔸 fetch
EAGER (default) → load immediately
LAZY → load only when needed (better for performance)
🔸 optional
true → Profile can be null
false → Profile MUST exist
🔸 referencedColumnName
Which column of Profile to refer (default = id)
🔸 nullable
false → must have profile
true → optional
🔸 unique
Ensures one-to-one at DB level

cascade = {
    CascadeType.PERSIST,
    CascadeType.MERGE,
    CascadeType.REMOVE,
    CascadeType.REFRESH,
    CascadeType.DETACH
}

Type	Action
PERSIST	save
MERGE	update
REMOVE	delete
ALL	everything

✅ orphanRemoval
@OneToOne(orphanRemoval = true)

👉 If you remove profile from user:

```
2. OneToMany ManyToOne
```java
User{
    @Id
    private int id;

    @OneToMany(manageby="user",cascade=CascadeType.All)
    private List<Post> post;
}

Post{
    @Id
    private int id;

    @ManyToOne()
    @JoinColumn(name="user_id")
    private User user;
}

```

@ManyToOne is owner

3. ManyToMany
```java
Post{
    @Id
    private int id;

    @ManyToOne()
    @JoinColumn(name="user_id")
    private User user;

    @ManyToMany()
    @JoinTable(
        name="post_tags"
        joinColumn=@JoinColumn(name="post_id")
        inverseJoinColumn=@JoinColumn(name="tag_id")
    )
    private List<Tag> tag;
}

Tag{
     @Id
    private int id;


    @ManyToMany(mappedBy="tags")
    private List<Post> posts;

}

```
###### application.properties
application.properties configure how your Spring Boot application behaves.

1️⃣ spring.application.name=demo
What it means

This gives a name to your application.

spring.application.name=demo
Why it exists

Spring Boot uses this name in:

logs

monitoring

microservices

Example

When your app starts you may see:

Starting demo application...

If you change it:

spring.application.name=myApp

Log becomes:

Starting myApp application...

Think of it like naming your project.

2️⃣ server.port=8080
What it means

This tells Spring Boot which port your server should run on.

server.port=8080
Example

Your application becomes available at:

http://localhost:8080

If you change it:

server.port=9090

Then it runs at:

http://localhost:9090
Simple analogy

Your computer = building
Port = door number

Computer
 └── Port 8080 → Spring Boot App

3️⃣ spring.datasource.url=jdbc:h2:mem:testDB

This tells Spring which database to use.

jdbc:h2:mem:testDB

Let's break it.

Part	Meaning
jdbc	Java database connection technology
h2	H2 database
mem	in-memory database
testDB	database name

What is H2?

H2 is a lightweight database used for testing.

What is mem?

mem means memory database.

So the database:

exists only while the app runs

disappears when the app stops

Example:

Start App → Database Created
Stop App → Database Deleted

4️⃣ spring.datasource.driverClassName=org.h2.Driver
What it means

This tells Java which driver to use to connect to the database.

Think of a driver like a translator.

Spring Boot → Driver → Database

Driver used here:

org.h2.Driver

Because we are using H2 database.

5️⃣ spring.datasource.username=sa

This is the database username.

H2 default user is:

sa

6️⃣ spring.datasource.password=

This is the database password.

H2 usually has no password, so it is empty.

username = sa
password = (empty)

7️⃣ spring.h2.console.enabled=true

This enables a web page where you can see the database.

Without this:

❌ you cannot view tables easily.

With this:

You can open:

http://localhost:8080/h2-console

Then you can:

see tables

run SQL queries

check stored data

Example query:

SELECT * FROM product;

Very useful for learning and debugging.

8️⃣ spring.jpa.show-sql=true

This tells Spring Boot:

👉 Print SQL queries in the console

Example.

If you save a product:

productRepository.save(product);

Console shows:

insert into product (name, price) values (?, ?)

Why useful?

You can see:

what queries are executed

if something is wrong

9️⃣ spring.jpa.hibernate.ddl-auto=update

This is VERY IMPORTANT.

It tells Hibernate how to manage database tables.

Here it is set to:

update

Meaning:

👉 If your entity changes, Spring updates the table automatically.

Example.

Entity:

@Entity
class Product {
    String name;
}

Table created:

product
 └── name

Later you add:

String price;

Spring automatically updates table:

product
 ├── name
 └── price

No manual SQL needed.

🔟 spring.jpa.properties.hibernate.format_sql=true

This makes SQL easier to read in logs.

Without formatting:

select product0_.id as id1_0_,product0_.name as name2_0_ from product product0_

With formatting:

select
    product0_.id,
    product0_.name
from
    product product0_

Much cleaner.

Spring Boot → JDBC URL → Driver → Database

The URL tells Java which database to connect to, and the driver is the software that understands that database.

1️⃣ H2 Database (In-Memory)

Example:

spring.datasource.url=jdbc:h2:mem:testDB
spring.datasource.driverClassName=org.h2.Driver

Explanation:

Part	Meaning
jdbc	Java database connection
h2	H2 database
mem	stored in memory
testDB	database name

Behavior:

Start app → database created
Stop app → database deleted

Good for testing.

2️⃣ H2 Database (File Based)

Instead of memory, you can store data in a file.

spring.datasource.url=jdbc:h2:file:./data/testDB
spring.datasource.driverClassName=org.h2.Driver

Behavior:

Start app → database loaded from file
Stop app → data remains saved
3️⃣ MySQL Database

Example:

spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.driverClassName=com.mysql.cj.jdbc.Driver
spring.datasource.username=root
spring.datasource.password=1234

Breakdown:

jdbc:mysql://host:port/database

Example:

localhost → database server
3306 → MySQL port
mydb → database name

Driver:

com.mysql.cj.jdbc.Driver
4️⃣ PostgreSQL Database

Example:

spring.datasource.url=jdbc:postgresql://localhost:5432/mydb
spring.datasource.driverClassName=org.postgresql.Driver

Driver:

org.postgresql.Driver
5️⃣ Oracle Database

Example:

spring.datasource.url=jdbc:oracle:thin:@localhost:1521:xe
spring.datasource.driverClassName=oracle.jdbc.OracleDriver
6️⃣ SQL Server

Example:

spring.datasource.url=jdbc:sqlserver://localhost:1433;databaseName=mydb
spring.datasource.driverClassName=com.microsoft.sqlserver.jdbc.SQLServerDriver
🔑 Important Rule

The URL format and driver must match the database.

Database	            URL Example	                                Driver
H2	                    jdbc:h2:mem:testDB	                        org.h2.Driver
MySQL	                jdbc:mysql://localhost:3306/mydb	        com.mysql.cj.jdbc.Driver
PostgreSQL	            jdbc:postgresql://localhost:5432/mydb    	org.postgresql.Driver
Oracle	                jdbc:oracle:thin:@localhost:1521:xe	        oracle.jdbc.OracleDriver
SQL Server	            jdbc:sqlserver://localhost:1433	            com.microsoft.sqlserver.jdbc.SQLServerDriver


###### ✅ Cascade in JPA / Hibernate — Short Summary

👉 What is Cascade?
**Cascade** means:

> Actions performed on the **parent entity** automatically apply to its **child entities**.

Example:  
If you save an `Order`, its `OrderItems` are saved automatically.

---

🔑 Main Cascade Types

✅ CascadeType.PERSIST
- Automatically **inserts child records** when the parent is saved.
- Does NOT update existing records.

🧠 **Memory Trick:** *Insert together.*

---

✅ CascadeType.MERGE
- Automatically **updates child records** when the parent is updated.
- Synchronizes detached objects with the database.

🧠 **Memory Trick:** *Update together.*

---

✅ CascadeType.REMOVE
- Automatically **deletes child records** when the parent is deleted.
- ⚠️ No safety check — deletes blindly.

🧠 **Memory Trick:** *Delete together.*

---

✅ CascadeType.ALL
Includes:
- PERSIST  
- MERGE  
- REMOVE  
- REFRESH  
- DETACH  

⚠️ Powerful but risky — use carefully.

🧠 **Memory Trick:** *Do everything.*

---

⭐ Golden Rule
👉 **Use cascade ONLY when the child cannot exist without the parent.**


#### Controller
```java
@RestController()
@RequestMapping("/api/categories")
public class CategoryController {


}

** Repository = Database operations **
** Mapper = Object conversion (Entity ↔ DTO) **

Stram
 .stream()
        .map(product -> {
            ProductDto dto = new ProductDto();
            dto.setId(product.getId());
            dto.setName(product.getName());
            return dto;
        })
        .toList()

```

###### EndPoint Mapping
@RequestMapping("/v2")
@PostMapping("/create")
@PostMapping({"/v1/create", "/v2/create"})


###### 📘 Java Optional

🔥 1. orElseThrow (for errors)

```java
Category category = repo.findById(id)
    .orElseThrow(() -> new RuntimeException("Category not found"));
```

✔ Use when value is required
✔ Most used in service layer


⚡ 2. orElse (default value - eager)

```java
Category category = repo.findById(id)
    .orElse(new Category("Default"));
```

⚠️ Object created even if value exists


🚀 3. orElseGet (default value - lazy)

```java
Category category = repo.findById(id)
    .orElseGet(() -> new Category("Default"));
```

✔ Better than `orElse()`
✔ Runs only if value is missing


🔄 4. map (transform value)

```java
String name = repo.findById(id)
    .map(Category::getName)
    .orElse("No Name");
```

✔ Extract or convert safely


🔗 5. flatMap (avoid nested Optional)

```java
Optional<String> result = repo.findById(id)
    .flatMap(cat -> cat.getOptionalField());
```

✔ Use when method already returns Optional


👀 6. ifPresent (execute if exists)

```java
repo.findById(id)
    .ifPresent(cat -> System.out.println(cat.getName()));
```

⚡ 7. ifPresentOrElse (Java 9+)

```java
repo.findById(id)
    .ifPresentOrElse(
        cat -> System.out.println(cat.getName()),
        () -> System.out.println("Not found")
    );
```

###### HttpStatus
Use Case	       Status
Get data	       200
Create	           201
Delete	           204
Invalid input	   400
Not logged in	   401
No permission	   403
Not found	       404
Duplicate	       409
Validation error   422
Server error	   500

###### ResponseEntity
1. OK Response (200)
return ResponseEntity.ok(data);

2. Custom Status
return new ResponseEntity<>(data, HttpStatus.CREATED);

3. No Content (204)
return ResponseEntity.noContent().build();

4. Not Found (404)
return ResponseEntity.notFound().build();

5. Bad Request (400)
return ResponseEntity.badRequest().body("Invalid input");

📦 Adding Headers
HttpHeaders headers = new HttpHeaders();
headers.add("Custom-Header", "value");

return new ResponseEntity<>(data, headers, HttpStatus.OK);


1. Using Builder Pattern
return ResponseEntity
        .status(HttpStatus.CREATED)
        .header("X-App", "Demo")
        .body(data);

###### Repository functions
1. Basic CRUD Methods (Most Used)
findAll()                Get all records
findById(id)             Get one by ID (Optional)
existsById(id)           Check if exists
count()                  Total records
save(entity)             Insert or update
saveAll(list)            Bulk save
deleteById(id)           Delete by ID
delete(entity)           Delete entity
deleteAll()              Delete all records


2. Custom Query Methods (Very Common 🚀)
Spring auto-generates queries based on method names:

findByName(String name)
findByStatus(String status)
findByNameAndStatus(String name, String status)
findByPriceGreaterThan(double price)
findByCreatedAtBetween(Date start, Date end)

3. Pagination
Pageable pageable = PageRequest.of(0, 10, Sort.by("name").ascending());
categoryRepository.findAll(pageable);

Pageable pageable = PageRequest.of(page, size, Sort.by(sortBy).descending());
return categoryRepository.findAll(pageable);

Pageable pageable = PageRequest.of(0, 10);
Page<Category> result = categoryRepository.findByStatus("ACTIVE", pageable);

Pageable pageable = PageRequest.of(
    0,
    10,
    Sort.by("name").ascending().and(Sort.by("createdAt").descending())
);

Pageable pageable = PageRequest.of(0, 10);
categoryRepository.findByNameContaining("food", pageable);

4. Custom JPQL/SQL
@Query("SELECT c FROM Category c WHERE c.name = :name")
Category getByName(@Param("name") String name);

deleteByName(String name)

5. Optional Handling
Category category = categoryRepository.findById(id)
    .orElseThrow(() -> new RuntimeException("Not found"));

###### Params & Query
```java
@PostMapping("/update/{id}")
public ResponseEntity<CategoryDto> updateCategory(
        @PathVariable Long id,
        @RequestParam(required = false) String status,
        @RequestBody CategoryDto categoryDto) {

    return ResponseEntity.ok(
        categoryService.updateCategory(id, status, categoryDto)
    );
}
```

above
Rest api and h2 jdbc database 

### SQL DB Configuration

<dependency>
      <groupId>com.mysql</groupId>
      <artifactId>mysql-connector-j</artifactId>
      <scope>runtime</scope>
</dependency>

```bash
mvn clean install
```

add this in pom file form java spring boot initializer pom file

```
spring.application.name=demo
server.port=8080
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=mysql
spring.datasource.password=mysqlpass

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
```

```bash
sudo apt install mysql-server -y     # install MySQL
sudo systemctl start mysql           # start service
sudo systemctl enable mysql          # auto-start on boot
sudo mysql -u root -p                # login
mysqlpass                            # password , can we any
```
###### MY SQL GUI in linux
```bash
sudo snap install dbeaver-ce --classic
dbeaver
Host: localhost
Port: 3306
Database: mydb
Username: mysql (or root)
Password: your password
```

```sql

CREATE DATABASE mydb;

CREATE USER 'springuser'@'localhost' IDENTIFIED BY 'password123';

GRANT ALL PRIVILEGES ON mydb.* TO 'springuser'@'localhost';

FLUSH PRIVILEGES;

mysql -u springuser -p
```

👉 IDENTIFIED BY means:

➡️ “Set a password for this user”

👉 'user'@'host' = who + from where
👉 localhost = same machine
👉 % = anywhere
👉 IP = restricted access

### Global Exception handling
1. Optional

@Repository
public interface CategoryRepository extends JpaRepository<Category,Long> {
       Optional<Category> findByName(String name);
}

 Optional<Category> optional=categoryRepository.findByName(categoryDto.getName());
        if(optional.isPresent()){
            throw new RuntimeException("Category already exist");
}

or 
package com.example.demo.exception;

import org.springframework.http.HttpStatus;
import org.springframework.web.bind.annotation.ResponseStatus;

@ResponseStatus(value= HttpStatus.CONFLICT)
public class CategoryAlreadyExistsException extends  RuntimeException{
    
    public CategoryAlreadyExistsException(String message){
        super(message);
    }
}

  if(optional.isPresent()){
            throw new CategoryAlreadyExistsException("Category already exist");
  }

2. use try catch 

 @PostMapping({"/v1/create", "/v2/create"})
    public ResponseEntity<?> createCategory(@RequestBody CategoryDto categoryDto){
        try{
            CategoryDto savedCategory=this.categoryService.createCategoryService(categoryDto);
            return new ResponseEntity<>(savedCategory,HttpStatus.CREATED);
        }catch(CategoryAlreadyExistsException error){
return new ResponseEntity<>(error.getMessage(),HttpStatus.CONFLICT);            
        }
    }

3. use apiResponse Class
public class ApiResponse<T> {
    private boolean success;
    private String message;
    private T data;

    public ApiResponse(boolean success, String message, T data) {
        this.success = success;
        this.message = message;
        this.data = data;
    }
}
@PostMapping({"/v1/create", "/v2/create"})
public ResponseEntity<ApiResponse<CategoryDto>> createCategory(@RequestBody CategoryDto categoryDto) {
    try {
        CategoryDto savedCategory = this.categoryService.createCategoryService(categoryDto);

        return ResponseEntity.status(HttpStatus.CREATED)
                .body(new ApiResponse<>(true, "Category created", savedCategory));

    } catch (CategoryAlreadyExistsException error) {
        return ResponseEntity.status(HttpStatus.CONFLICT)
                .body(new ApiResponse<>(false, error.getMessage(), null));
    }
}

4. global exception handling

```java
package com.example.demo.exception;

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;

import java.lang.module.ResolutionException;

@ControllerAdvice
public class GlobalExceptionHandler {
    
    
    @ExceptionHandler(CategoryAlreadyExistsException.class)
    public ResponseEntity<String> handleCategoryAlreadyExistsException(CategoryAlreadyExistsException ex){
        return new ResponseEntity<>(ex.getMessage(),HttpStatus.CONFLICT);
        
    }
    
}
```

or
if want to handle all runtime exception
```java
@ExceptionHandler(RuntimeException.class)
public ResponseEntity<String> handleRuntimeException(RuntimeException ex){
    return new ResponseEntity<>(ex.getMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
}
```

###### web request
```java

@ControllerAdvice
public class GlobalExceptionHandler {
    
    
    @ExceptionHandler(CategoryAlreadyExistsException.class)
    public ResponseEntity<String> handleCategoryAlreadyExistsException(CategoryAlreadyExistsException ex,WebRequest webReqest){
        
        return new ResponseEntity<>(ex.getMessage(),HttpStatus.CONFLICT);
        
    }
    
}

webRequest.getDescription(false)  // TO GET API PATH
String token = webRequest.getHeader("Authorization");
String id = webRequest.getParameter("id");
Iterator<String> params = webRequest.getParameterNames();
Object attr = webRequest.getAttribute("name", WebRequest.SCOPE_REQUEST);

String path = webRequest.getDescription(false).replace("uri=", "");


or

@ExceptionHandler(RuntimeException.class)
public ResponseEntity<ErrorResponse> handleRuntimeException(
        RuntimeException ex,
        HttpServletRequest request) {

    String path = request.getRequestURI();

    return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
            .body(new ErrorResponse(ex.getMessage(), path));
}

request.getRequestURI();   // /v1/create
request.getMethod();       // POST
request.getRemoteAddr();   // IP
request.getHeader("Authorization");
request.getQueryString();
```

### swagger 
4.30
it a tool used to share api documention to other developers
