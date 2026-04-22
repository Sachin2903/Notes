# Java 8
is build to concise and minimal code
to utilize functional programing benefits in JAVA , JAVA 8 came 

### Lambda expression
it is an anonymous function

steps to make any function lambda expression
remove modifier -> return type -> method name -> place arrow
no needs to use return if single statement
can skip () on single parameter
```java
()->{

}

(int a , int b)-> {System.out.println(a+b);}
( a , b) -> System.out.println(a+b)
```

🔑 Access Modifier Summary
Modifier	Same Class	Same Package	Subclass (diff pkg)	   Other Package
public	         ✅	       ✅	             ✅	             ✅
protected	     ✅	       ✅	             ✅*	             ❌
default	         ✅	       ✅	             ❌	             ❌
private	         ✅	       ❌	             ❌	             ❌

### Functional Interface
Interface having exactly single abstract method but can have any number of defaults and static methods. we can invoke lambda expression by using functional interface.

default method that have body 
@FunctionalInterface
public interface MyInterface{
    public void sayHello();

    default void sayBye(){}

    public static void sayOk(){

    }
}

@FunctionalInterface
public interface Employee {
    String getJobTitle();
}

// we are defining functionality of functional  interface abstract method
Employee employee = ()->"SOftware Engineer";
or
Employee employee = new Employee() {
    @Override
    public String getJobTitle() {
        return "Software Engineer";
    }
};

>> with anonymous class we can ovverride method functinality of interface 

interface Employee{

}

Employee emp=new Employee()'


A thread is the smallest unit of execution inside a program.
It allows a program to run multiple tasks at the same time.

Thread thread = new Thread(() -> {
    System.out.println("Thread is running");
});

Thread thread = () -> {
    System.out.println("Thread is running");
};

thread.start();

##### Comparator
Collection.sort(list,(a,b)->b-a)
can can have 
TreeSet,treemap,list,array

array
Array.sort(array,(a,b)=>a-b);

##### Predicates
its is an functional interface that have a boolean return test named function

test -> boolean return function

```java
  Predicate<Integer> predicate = new Predicate<Integer>() {
            @Override
            public boolean test(Integer x) {
                return x % 2 == 0;
            }
        };
```

# 📘 Java List + Stream Chain Methods (Complete Cheat Sheet)

---

# 🔹 1. List Creation + Properties

🔹 1. Key Properties
Mutable → can modify (add/remove/update)
Immutable → cannot change after creation
Resizable → can change size (add/remove elements)

### ✅ ArrayList

```java
List<Integer> list = new ArrayList<>();
```

* Mutable ✅ | Resizable ✅

---

### ✅ LinkedList

```java
List<Integer> list = new LinkedList<>();
```

* Mutable ✅ | Resizable ✅

---

### ⚠️ Arrays.asList()

```java
List<Integer> list = Arrays.asList(1, 2, 3);
```

* Mutable (set allowed) ✅ | Resizable ❌

---

### ❌ List.of()

```java
List<Integer> list = List.of(1, 2, 3);
```

* Immutable ❌ | Resizable ❌

---

### ❌ Stream.toList()

```java
List<Integer> list = Stream.of(1, 2, 3).toList();
```

* Immutable ❌ | Resizable ❌

---

# 🔹 2. Stream Pipeline

```java
list.stream()
```

👉 Structure:

```
stream → intermediate ops → terminal op
```

---

# 🔹 3. Intermediate Operations (Chain Methods)

### 🔸 Filtering

```java
.filter(x -> x > 2)
.distinct()
.limit(3)
.skip(1)
.takeWhile(x -> x < 5)
.dropWhile(x -> x < 5)
```

---

### 🔸 Mapping / Transformation

```java
.map(x -> x * 2)
.mapToInt(x -> x)
.mapToDouble(x -> x)
.mapToLong(x -> x)
.flatMap(x -> Stream.of(x, x * 2))
```

---

### 🔸 Sorting

```java
.sorted()
.sorted((a, b) -> b - a)
```

---

### 🔸 Peek (debugging)

```java
.peek(System.out::println)
```

---

# 🔹 4. Terminal Operations

### 🔸 Collection / Output

```java
.collect(Collectors.toList())
.toList()
.forEach(System.out::println)
```

---

### 🔸 Numeric

```java
.sum()
.average()
.min()
.max()
```

---

### 🔸 Counting

```java
.count()
```

---

### 🔸 Finding

```java
.findFirst()
.findAny()
```

---

### 🔸 Matching

```java
.anyMatch(x -> x > 5)
.allMatch(x -> x > 0)
.noneMatch(x -> x < 0)
```

---

### 🔸 Reduce (custom logic)

```java
.reduce(0, (a, b) -> a + b)
```

---

# 🔹 5. Example Full Chain

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

int result = numbers.stream()
    .filter(n -> n % 2 == 0)
    .map(n -> n * 2)
    .sorted((a, b) -> b - a)
    .limit(2)
    .mapToInt(n -> n)
    .sum();
```

---

# 🔹 6. Advanced Useful Methods

```java
.collect(Collectors.groupingBy(x -> x % 2))
.collect(Collectors.partitioningBy(x -> x % 2 == 0))
.collect(Collectors.joining(","))
```

---

---

```java
Predicate<String> startWithLetterV=x->x.toLowerCase().charAt(0)=="v";
Predicate<String> endWithLetterL=x->x.toLowerCAse().charAt(x.length()-1)=="l";

and function combine one prediation boolean with another 
Predicate<String> and =startsWithLetterV.and(endsWithLetterL);
System.out.println(and.test("Vipul"));


startsWithLetterV.negate().test("Vipul");
```

##### Function 
it simillar to prediate have a generic return type function

```java
Function<String,Integer> function1=x->x.length();
Function<String,Integer> function2=x->x.toUpperCase();
function.apply("vipul");

function chaning
Function<String,String> Function<String,String> stringStringFunction=stringStringFunction=function1.andThen(function2);

or function1.andThen(function2).apply();


function2.andThen(function1).apply();
or
just reverse thing
function1.compose(function2).apply(3)
stringStringFunction.apply("vipul");

It returns a function that simply returns the input as it is.
Function<String, String> func = Function.identity();

System.out.println(func.apply("Hello")); 
Hello
```

##### Consumer Interface
it void return type accept method

```java
Consumer<String> consumer=s->System.out.println(s);

consumer.accept("vipul");
and can use andThen and as it retunr a new consumer so we can use or accept it

```
##### Runnable?

Runnable is a functional interface in Java that represents a task that can be executed.

It has just one method:

void run();

##### supplier functional interface
it has a get abstract method

```java
Supplier<Integer> supplier = () -> 1;
suuplier.get();

```

##### BiPredicate , BiFunction BiConsumer
Predicate have single argument where biPredicate can have 2 arguments 
same as with BIFunction and BiCOnsumer

##### UnaryOperator && Binary Operator
uniary operator extends function functional interface
it use when pass and return type are same 
UNaryOperator<Integer> uniaryOperator=x->x.length();

BInaryOperaor is same as uniary but when we work we 2 argumanet

##### Method and constructor reference
:: is called method reference
Public

1. ClassName::method
String::length (String s) -> s.length()
String::toUpperCase  x -> x.toUpperCase()
System.out::println
.forEach(System.out::println);

2.Constructor reference
BiFunction<Integer, Integer, ArrayList> func = ArrayList::new;

(a, b) -> new ArrayList(a)

.parallelStream() is same as stream but it works on chunks thread


##### Optonal
Optional<String> opt1 = Optional.of("Hello");     // ❌ Null not allowed
Optional<String> opt2 = Optional.ofNullable(null); // ✅ Can handle null
Optional<String> opt3 = Optional.empty();         // Empty Optional

opt.isPresent();   // true/false
opt.isEmpty();     // Java 11+

Optional<String> name = Optional.of("Sachin");

Optional<Integer> length = name.map(String::length);


Optional<User> user = Optional.of(new User());

Optional<Address> address =
    user.flatMap(User::getAddress);

    opt.ifPresent(val -> System.out.println(val));

opt.ifPresentOrElse(
    val -> System.out.println(val),
    () -> System.out.println("No value")
);

Optional<Integer> num = Optional.of(10);

num.filter(n -> n > 5)
   .ifPresent(System.out::println);

Optional<User> user = findUserById(id);

String city = user
    .map(User::getAddress)
    .map(Address::getCity)
    .orElse("Unknown");

String str = "abc";

str.chars()
   .mapToObj(c -> (char) c)   // int → char
   .forEach(System.out::println);