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
@Component , @Bean , @Configuration , @Controller , @RestController , @Service , @Repository, @Entity

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

@Value()

1.
@Value("10")
private int a;

2. 
public HelperClass(@Value("10") int a) {
    this.a = a;
}

3.
@Bean
public MyBean myBean(@Value("10") int a) {
    return new MyBean(a);
}

application properties
app.numbers=1,2,3,4
app.names=Sachin,Rahul,Amit

@Value("${app.numbers}")
private int[] numbers;

@Value("${app.names}")
private List<String> names;

@Value("#{'${app.names}'.split(',')}")
private List<String> names;

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

👉 If you remove profile from user: profile becomes orphan so hibernate remove it auto

```
2. OneToMany ManyToOne
```java
User{
    @Id
    private int id;

    @OneToMany(mappedBy="user",cascade=CascadeType.All)
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
2️⃣ server.port=8080
3️⃣ spring.datasource.url=jdbc:h2:mem:testDB

Part	Meaning
jdbc	Java database connection technology
h2	H2 database
mem	in-memory database
testDB	database name

4️⃣ spring.datasource.driverClassName=org.h2.Driver

Spring Boot → Driver → Database
spring auto detect driver

5️⃣ spring.datasource.username=sa
6️⃣ spring.datasource.password=
7️⃣ spring.h2.console.enabled=true

This enables a web page where you can see the database.

Without this:

❌ you cannot view tables easily.

With this:

You can open:

http://localhost:8080/h2-console

8️⃣ spring.jpa.show-sql=true
9️⃣ spring.jpa.hibernate.ddl-auto=update
👉 If your entity changes, Spring updates the table automatically.

🔟 spring.jpa.properties.hibernate.format_sql=true

This makes SQL easier to read in logs.

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
SQL Server	            jdbc:sqlserver://localhost:1433	            com.microsoft.sqlserver.jdbc.SQLServerDriver+

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
List<User> findByName(String name);
User findByEmail(String email);
List<User> findByAgeGreaterThan(int age);
List<User> findByNameAndStatus(String name, String status);
User user = userRepository.findTopByName(String name);
User user = userRepository.findFirstByName(String name);

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
```bash
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.5.0</version>
</dependency>
```

http://localhost:8080/swagger-ui.html


```java
@OpenAPIDefinition(
    info = @Info(
        title = "My API",
        version = "1.0",
        description = "API documentation using Swagger",
        termsOfService = "https://example.com/terms",
        contact = @Contact(
            name = "Sachin",
            email = "sachin@example.com"
        ),
        license = @License(
            name = "Apache 2.0",
            url = "https://apache.org"
        )
    ),
    servers = {
        @Server(url = "http://localhost:8080", description = "Local"),
        @Server(url = "https://api.prod.com", description = "Production")
    },
    tags = {
        @Tag(name = "Auth", description = "Authentication APIs"),
        @Tag(name = "User", description = "User APIs")
    },
    security = {
        @SecurityRequirement(name = "bearerAuth")
    }
)
@SecurityScheme(
    name = "bearerAuth",
    type = SecuritySchemeType.HTTP,
    scheme = "bearer",
    bearerFormat = "JWT"
)
@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

## Spring Security
### Basic Auth
simple method where user privide a userame and password with each request

>> Authentication && Authorization

1. add security dependency

```xml
<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>
		</dependency>
```
>> after adding this no api will return data
to use api we need a password and a user password will be shared in terminal once above dependecy run and can be used in authorization basic auth username and password

```java
@Configuration
@EnableWebSecurity
@EnableMethodSecurity(prePostEnabled = true)
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilter(HttpSecurity http) throws Exception {
        http.csrf(csrf -> csrf.disable())
                .authorizeHttpRequests(request -> request
                        .requestMatchers(HttpMethod.GET, "/api/**").permitAll()
                        .anyRequest().authenticated()
                );

        return http.build();
    }

    @Bean
    public PasswordEncoder passwordEncoder(){
        return new BCryptPasswordEncoder();
    }

    @Bean
    public UserDetailsService userDetailsService() {
        UserDetails admin = User.builder().username("admin").password(passwordEncoder().encode("admin")).roles("ADMIN").build();
        UserDetails seller = User.builder().username("seller").password(passwordEncoder().encode("seller")).roles("SELLER").build();

        return new InMemoryUserDetailsManager(admin,seller);

    }
}


// Authorization
@PreAuthorize("hasAuthority('ROLE_ADMIN')")
@PreAuthorize("hasAnyRole('ADMIN','SELLER')")
@PreAuthorize("hasAnyRole('ADMIN','SELLER')")
@PreAuthorize("hasRole('ADMIN')")
@PreAuthorize("#id == authentication.principal.id")

@PostMapping({"/v1/create", "/v2/create"})

@PreAuthorize("hasRole('ADMIN') or hasRole('SELLER')")
@PostMapping("/product")
public void addProduct() {}


@PostAuthorize("returnObject.owner == authentication.name")
@GetMapping("/order/{id}")
public Order getOrder(@PathVariable Long id) {
    return orderService.getOrder(id);
}
 this use to block the respnose

.requestMatchers("/admin/**").hasRole("ADMIN")
.requestMatchers("/seller/**").hasAnyRole("SELLER", "ADMIN")
```

###### credential in DB
```java
@Entity
public class User {

    @Id
    @GeneratedValue
    private Long id;

    private String username;
    private String password;
    private String role; // e.g. ROLE_ADMIN

}

public interface UserRepository extends JpaRepository<User, Long> {
    Optional<User> findByUsername(String username);
}

@Service
public class MyUserService implements UserDetailsService {


    @Autowired
    private UserRepository userRepository;

    public User createUser(User user){
        return userRepository.save(user);
    }

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
      Optional<User> user=userRepository.findByUsername(username);
      if(user.isEmpty()){
          throw   new UsernameNotFoundException("user not found");
      }
        return org.springframework.security.core.userdetails.User.builder()
                .username(user.get().getUsername())
                .password(user.get().getPassword())
                .authorities(
                        user.get().getRoles().stream()
                                .map(role -> new SimpleGrantedAuthority("ROLE_" + role))
                                .toList()
                )
                .build();
    }
}

we use this new SimpleGrantedAuthority  because spring requires an object

use of this .authorities(user.getRole())
.requestMatchers("/api/data")
.hasAnyRole("USER", "ADMIN")

// this create  aseperate table
@ElementCollection(fetch = FetchType.EAGER)
    @CollectionTable(name = "user_roles", joinColumns = @JoinColumn(name = "user_id"))
    @Column(name = "role")
    private List<String> roles;

@Configuration
@EnableWebSecurity
public class SecurityConfig {

    private final CustomUserDetailsService userDetailsService;

    public SecurityConfig(CustomUserDetailsService userDetailsService) {
        this.userDetailsService = userDetailsService;
    }

      @Bean
    public SecurityFilterChain securityFilter(HttpSecurity http) throws Exception {
        http.csrf(csrf -> csrf.disable())
                .authorizeHttpRequests(request -> {
                    request.requestMatchers(HttpMethod.GET, "/api/**").permitAll();
                            request.anyRequest().authenticated();
                        }
                ).authenticationProvider(authenticationProvider())
                .httpBasic(Customizer.withDefaults());

        return http.build();
    }

    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    @Bean
    public DaoAuthenticationProvider authProvider() {
        DaoAuthenticationProvider provider = new DaoAuthenticationProvider();
        provider.setUserDetailsService(userDetailsService);
        provider.setPasswordEncoder(passwordEncoder());
        return provider;
    }

     public AuthenticationManager authenticationManager(AuthenticationConfiguration config) throws Exception {
        return config.getAuthenticationManager();

    }
}

Authentication auth = authenticationManager.authenticate(
    new UsernamePasswordAuthenticationToken(username, password)
);

if (auth.isAuthenticated()) {
    String token = jwtService.generateToken(username);
    return token;
}

Request → Security Filter → AuthenticationManager
        → AuthenticationProvider
        → UserDetailsService



    @Bean
    public PasswordEncoder passwordEncoder(){
        return new BCryptPasswordEncoder(12);
    }

can pass strength 

```

or

```java
 @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
      Optional<User> user=userRepository.findByUsername(username);
      if(user.isEmpty()){
          throw   new UsernameNotFoundException("user not found");
      }
        return new UserPrinciple(user.get());
    }
public class UserPrinciple implements UserDetails {

    private final User user;

    public UserPrinciple(User user){
        this.user=user;
    }

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        return List.of(new SimpleGrantedAuthority("ROLE_SELLER"));
    }

    @Override
    public String getPassword() {
        return user.getPassword();
    }

    @Override
    public String getUsername() {
        return user.getUsername();
    }
}
```

### JWT TOKEN Based Authentication
JSON web token is a secure way to send information between two parties

it contain header, payload , signature

```java
@Entity
public class RefreshToken {

    @Id
    @GeneratedValue
    private Long id;

    private String token;

    private String username;

    private Instant expiryDate;
}

public interface RefreshTokenRepository extends JpaRepository<RefreshToken, Long> {
    Optional<RefreshToken> findByToken(String token);
}
@Service
public class RefreshTokenService {

    @Autowired
    private RefreshTokenRepository repo;

    public RefreshToken createRefreshToken(String username) {
        RefreshToken token = new RefreshToken();
        token.setUsername(username);
        token.setToken(UUID.randomUUID().toString());
        token.setExpiryDate(Instant.now().plus(7, ChronoUnit.DAYS));
        return repo.save(token);
    }

    public RefreshToken verifyToken(String token) {
        RefreshToken rt = repo.findByToken(token)
                .orElseThrow(() -> new RuntimeException("Invalid refresh token"));

        if (rt.getExpiryDate().isBefore(Instant.now())) {
            repo.delete(rt);
            throw new RuntimeException("Refresh token expired");
        }

        return rt;
    }
}

```


```bash
	<dependency>
			<groupId>io.jsonwebtoken</groupId>
			<artifactId>jjwt-api</artifactId>
			<version>0.11.5</version>
		</dependency>

		<dependency>
			<groupId>io.jsonwebtoken</groupId>
			<artifactId>jjwt-impl</artifactId>
			<version>0.11.5</version>
			<scope>runtime</scope>
		</dependency>

		<dependency>
			<groupId>io.jsonwebtoken</groupId>
			<artifactId>jjwt-jackson</artifactId>
			<version>0.11.5</version>
			<scope>runtime</scope>
		</dependency>
```

```java
@PostMapping("/login")
public AuthResponse login(@RequestBody LoginRequest req) {

    Authentication auth = authenticationManager.authenticate(
        new UsernamePasswordAuthenticationToken(
            req.getUsername(),
            req.getPassword()
        )
    );

    UserDetails user = (UserDetails) auth.getPrincipal();

    String accessToken = jwtService.generateToken(user);
    RefreshToken refreshToken = refreshTokenService.createRefreshToken(user.getUsername());

    return new AuthResponse(
            accessToken,
            refreshToken.getToken(),
            user.getUsername()
    );
}

@PostMapping("/refresh")
public AuthResponse refresh(@RequestBody String refreshToken) {

    RefreshToken rt = refreshTokenService.verifyToken(refreshToken);

    UserDetails user = userDetailsService.loadUserByUsername(rt.getUsername());

    String newAccessToken = jwtService.generateToken(user);

    return new AuthResponse(
            newAccessToken,
            refreshToken,
            user.getUsername()
    );
}


```

```java

@Component
public class JwtRequestFilter extends OncePerRequestFilter {

    @Autowired
    private JwtService jwtService;

    @Autowired
    private UserDetailsService userDetailsService;

    @Override
    protected void doFilterInternal(
            HttpServletRequest request,
            HttpServletResponse response,
            FilterChain filterChain)
            throws ServletException, IOException {

        final String authHeader = request.getHeader("Authorization");

        String username = null;
        String token = null;

        // 1. Extract token
        if (authHeader != null && authHeader.startsWith("Bearer ")) {
            token = authHeader.substring(7);
            username = jwtService.extractUsername(token);
        }

        // 2. Validate and set authentication
        if (username != null && SecurityContextHolder.getContext().getAuthentication() == null) {

            UserDetails userDetails = userDetailsService.loadUserByUsername(username);

            if (jwtService.validateToken(token, userDetails)) {

                UsernamePasswordAuthenticationToken authToken =
                        new UsernamePasswordAuthenticationToken(
                                userDetails,
                                null,
                                userDetails.getAuthorities()
                        );

                SecurityContextHolder.getContext().setAuthentication(authToken);
            }
        }

        // 3. Continue request
        filterChain.doFilter(request, response);
    }
}


@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Autowired
    private JwtRequestFilter jwtRequestFilter;

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {

        http
            .csrf(csrf -> csrf.disable())
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/user/login", "/user/register").permitAll()
                .anyRequest().authenticated()
            )
            .addFilterBefore(jwtRequestFilter, UsernamePasswordAuthenticationFilter.class);

        return http.build();
    }
}
```

### OAuth2 


###  📘 Logging & Actuator (Quick Notes)

* Records app events (info, debug, errors)
* Default: **Logback**

#####  Usage

```java
Logger log = LoggerFactory.getLogger(MyClass.class);
log.info("Info");
log.debug("Debug");
log.error("Error");
```

#####  Levels

TRACE < DEBUG < INFO < WARN < ERROR

#####  Config

```properties
logging.level.root=INFO
logging.level.org.springframework.security=DEBUG
logging.file.name=app.log
```

---

####  🔹 Actuator

* Monitoring & management endpoints

#####  Dependency

```xml
spring-boot-starter-actuator
```

#####  Common Endpoints

* `/actuator/health`
* `/actuator/info`
* `/actuator/beans`
* `/actuator/loggers`

#####  Enable

```properties
management.endpoints.web.exposure.include=*
```

#####  Production (safe)

```properties
management.endpoints.web.exposure.include=health,info
```

---

######  🔥 Combo (Power Feature)

Change log level at runtime:

```
POST /actuator/loggers/{package}
{
  "configuredLevel": "DEBUG"
}
```

---


#### JPQL & QUERY Methods
 findByName
 Patient findByBirthDateOrEmail() 
 List<Patient> findByBirthDateOrEmail() 
 findDistinctByName
##### Query Methods (jp query methods)

###### Distinct

findDistinctByLastnameAndFirstname

select distinct …​ where x.lastname = ?1 and x.firstname = ?2

###### And

findByLastnameAndFirstname

… where x.lastname = ?1 and x.firstname = ?2

###### Or

findByLastnameOrFirstname

… where x.lastname = ?1 or x.firstname = ?2

###### Is, Equals

findByFirstname,findByFirstnameIs,findByFirstnameEquals

… where x.firstname = ?1 (or … where x.firstname IS NULL if the argument is null)

###### Between

findByStartDateBetween

… where x.startDate between ?1 and ?2

###### LessThan

findByAgeLessThan

… where x.age < ?1

###### LessThanEqual

findByAgeLessThanEqual

… where x.age <= ?1

###### GreaterThan

findByAgeGreaterThan

… where x.age > ?1

###### GreaterThanEqual

findByAgeGreaterThanEqual

… where x.age >= ?1

###### After

findByStartDateAfter

… where x.startDate > ?1

###### Before

findByStartDateBefore

… where x.startDate < ?1

###### IsNull, Null

findByAge(Is)Null

… where x.age is null

###### IsNotNull, NotNull

findByAge(Is)NotNull

… where x.age is not null

###### Like

findByFirstnameLike

… where x.firstname like ?1

###### NotLike

findByFirstnameNotLike

… where x.firstname not like ?1

###### StartingWith

findByFirstnameStartingWith

… where x.firstname like ?1 (parameter bound with appended %)

###### EndingWith

findByFirstnameEndingWith

… where x.firstname like ?1 (parameter bound with prepended %)

###### Containing

findByFirstnameContaining

… where x.firstname like ?1 (parameter bound wrapped in %)

###### OrderBy

findByAgeOrderByLastnameDesc

… where x.age = ?1 order by x.lastname desc

###### Not

findByLastnameNot

… where x.lastname <> ?1 (or … where x.lastname IS NOT NULL if the argument is null)

###### In

findByAgeIn(Collection<Age> ages)

… where x.age in ?1

###### NotIn

findByAgeNotIn(Collection<Age> ages)

… where x.age not in ?1

###### True

findByActiveTrue()

… where x.active = true

###### False

findByActiveFalse()

… where x.active = false

###### IgnoreCase

findByFirstnameIgnoreCase

… where UPPER(x.firstname) = UPPER(?1)

##### JPQL 
JPQL (Java Persistence Query Language) is used in Spring Boot / JPA to query entities (Java objects) instead of database tables.

@Query("SELECT p FROM Patient p WHERE p.bloodGroup = ?1")
List<Patient> findByBloodGroup(BloodGroupType bloodGroup);

@Query("SELECT p FROM Patient p WHERE p.bloodGroup = :bloodGroup")
List<Patient> findByBloodGroup(@Param("bloodGroup") BloodGroupType bloodGroup);

###### Group by query

@Query("select p.bloogGroup Count(p) from patient p group by p.bloodgroup")
List<Object[]> countEachBloodGroupType(@Param("bloodGroup") BloodGroupType bloodGroupType);

for(Object[] object:bloodGroupList){
    System.out.println(object[0]+" "+object[1]);
}

###### Native query pure sql query

@Query(value="select * from patient",nativeQuery=true)
List<Patient> findAllPatients();

###### Modify QUery

@Transactional 
@Modifying
@Query("UPDATE Patient p Set p.name = :name where p.id= :id")
int updateNameWithId(@Param("name") String name,@Param("id") Long id;)

###### Projection

public class BloodGroupCountResponseEntity{
    private BloodGroupType bloodGroupType;
    private Long count;
}

copy reference

```java
@Query("SELECT new com.yourpackage.BloodGroupCountResponseEntity(p.bloodGroup, COUNT(p)) " +
       "FROM Patient p " +
       "GROUP BY p.bloodGroup")
List<BloodGroupCountResponseEntity> countEachBloodGroupType();
```

this can not done with native query 

##### Paggination




