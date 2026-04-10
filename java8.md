+# Java 8
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

thread.start();

##### Comparator
Collection.sort(list,(a,b)->b-a)

TreeSet,hashSet

##### Predicates
its is an functional interface that have a boolean return test named function

test -> boolean return function


List<Integer> numbers=Arrays.asList(1,2,3,4);
numers.stream().filter(n->n%2==0).mapToInt(n->n).sum();;

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

##### Stream
collection to steam and do declarative and functional operation

if want to use
map , filter , reduce
need to convert collection to steam
Arrays.stream(array).filter(x->x%2==0).sum()
or
list.stream()
or
Stream.off(1,2,3);
Stream<Integer> integerStream = Stream.off(1,2,3);
or
Steam.iterate(0,n->n+1).limit(100);
or
Stream.generate(()->"Hello").limit(5);

###### filter
list.stream().filter(x->x%2==0).collect(Collectors.toList());
###### map
.map(x->xx/2)
###### distinct
.distinct()
to remove repetition
###### sorted
.sorted((a,b)->a-b)
###### skip
.skip(1)
###### peek
.peek(x->System.out.println(x));

.min()
.max((a,b)=>a-b).get()
.count()

.parallelStream() is same as stream but it works on chunks thread





