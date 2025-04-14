# Dart Programming Language Notes

Dart is a programming language developed by **Google**.  
It combines features of **JavaScript**, **Java**, and **Python**.

---

## Compilation Process

Dart uses two types of compilation to convert source code into machine code:

### 1. JIT (Just-In-Time)
- Used during **development**.
- Provides **fast iteration** and **immediate feedback**.
- Good for hot reload in Flutter apps.

### 2. AOT (Ahead-Of-Time)
- Used during **deployment**.
- Compiles Dart code into **optimized machine code**.
- Makes applications **efficient**, **fast**, and **production-ready**.

---

## Dart is a Typed Language

Every variable in Dart has a type. You can either specify it explicitly or let Dart infer it.

---

## Dart SDK

SDK = **Software Development Kit**  
Tools required for the system to understand and compile Dart code.

### You can use:
- **Flutter SDK** (includes Dart SDK) – for building apps using Flutter.
- **Dart SDK** – for running standalone Dart code.
- **[DartPad](https://dartpad.dev/)** – an online compiler to write and test Dart code in the browser.

---

## Hello World Example

```dart
void main() {
  for (var i = 0; i < 10; i++) {
    print('Hello ${i + 1}');
  }
}
```

---

## Print Statements

- `print("Hello World");`
- `print("Hello " + 2);` Not allowed – cannot concatenate a string with an integer directly.
- `print("Hello " * 2);` Prints the string twice: `Hello Hello`

---

## Comments

```dart
// This is a single-line comment

/*
 This is a
 multi-line comment
*/
```

---

## Variables and Types

### Integers
```dart
int age = 25;
print(age.isEven); // true or false
print(age.isOdd);  // true or false
```

### Strings
```dart
String name = "Sachin";
print(name.length);
print(name[0]); // S
```

### Booleans
```dart
bool isActive = true;
```

### Dynamic
```dart
dynamic value = 18.8;
print(value.runtimeType); // double

dynamic str="sachin";
  str="sachinasdas";
  str=true;
  print(str.runtimeType);
```

---

## Increment & Decrement

```dart
int x = 5;
x++; // x = 6
x--; // x = 5
```

---

## String Interpolation

```dart
String name = "Sachin";
print("Hello, $name");
print("2 + 2 = ${2 + 2}");
```

Use `\` to escape symbols:
```dart
print("Price is \$20");
```

---

## Multi-line Strings

Use triple quotes for multi-line text:

```dart
String message = """Hello,
This is a multi-line string.
""";
```

---

## `var`, `final`, and `const`

| Keyword | Description |
|--------|-------------|
| `var`  | Type is inferred from the value. Can be reassigned. |
| `final` | Single assignment. Runtime constant. |
| `const` | Compile-time constant. Immutable and reused. |

### Example:

```dart
var name = "Sachin"; // type inferred as String

final now = DateTime.now(); // value set at runtime

const pi = 3.14; // value must be known at compile-time
```

```dart
final a = [1, 2, 3];
final b = [1, 2, 3];
print(identical(a, b)); // false (different objects)

const c = [1, 2, 3];
const d = [1, 2, 3];
print(identical(c, d)); // true (same object)
```

Using `const` where possible improves performance by reducing memory usage.

---

# Dart Notes

## 🧹 Nullable Variables

- **Before Dart 2:**
  ```dart
  String some = null; // Allowed before Dart 2
  ```

- **Dart 2 and above:**
  ```dart
  String? str = null; // Nullable String
  String? str;
  late String str;

  print(str?.length); // Safe access
  print(null ?? 0);   // Null-aware operator
  ```

---

## 🔀 Control Flow

### if, else if, else
```dart
if (age >= 10) {
  print("Age is 10 or more");
} else if (age > 5) {
  print("Age is more than 5");
} else {
  print("Age is 5 or less");
}
```

---

## 🔧 Operators

- Assignment: `=`
- Equality: `==`
- Logical AND: `&&`
- Logical NOT: `!`

📝 **Note:**  
Dart doesn’t treat integers as truthy or falsy. They must be used with logical expressions like `if (num > 0)`.

---

## 🔤 String Methods

```dart
str.isEmpty;
str.isNotEmpty;
str.startsWith("A");
str.substring(1, 3);
can only be in the string range
```

---

## 🔁 Loops

### For Loop
```dart
for (int i = 0; i <= 10; i++) {
  print(i);
}
```

### While Loop
```dart
while (condition) {
  // loop body
}
```

### Do-While Loop
```dart
do {
  // loop body
} while (condition);
```

### Loop Controls
```dart
break;     // Exit the loop
continue;  // Skip current iteration
```

---

## 🧠 Switch Case

```dart
switch (value) {
  case "Hello":
    print("Greeting");
    break;
    
  case "Hi" when age >= 23:
    print("Hi and age >= 23");
    break;

  default:
    print("Default case");
}
```

📝 **Notes:**
- `break` is **only required** if the case has code.  
- Dart **did not support relational patterns** (`when`, `>=`, etc.) in `case` until Dart 3.

---

## 🔣 Functions

### Basic Syntax
```dart
ReturnType functionName() {
  // logic
  return value;
}
```

---

### Tuple Return (Destructuring Record)
```dart
void main() {
  var (age, name, isAdult, greeting) = printName();
  print(name); // prints "Riva"
}

(int, String, bool, String) printName() {
  return (12, "Riva", false, "Hi");
}
```

---

### Named Parameters
```dart
void main() {
  String name = "Ravan R.";
  printName(name: name, age: 12, greeting: "hello");
}

// Required named parameters
void printName({required String name, required int age, required String greeting}) {
  print("Hi $name, you are $age. $greeting");
}

// Optional named parameter
void printName({required String name, int? age, required String greeting}) {
  print("Hi $name, age: ${age ?? 'unknown'}. $greeting");
}

// Mixed: positional + named parameters
void printNameMixed(int age, {required String name}) {
  print("Hi $name, you are $age years old.");
}
```

---

### Returning Records with Named Fields
```dart
void main() {
  final stuff = printStuff();
  print(stuff.name);
  print(stuff.age);
}

({int age, String name}) printStuff() {
  return (age: 12, name: "Rivaan");
}
```

---

### Returning a Function from a Function
```dart
Function printStuff() {
  return () {
    print("Voo");
  };
}
```

---

### Anonymous Function
```dart
(() {
  print("hello");
})();
```

---

### Fat Arrow / Arrow Function
```dart
void functionName() => print("Hi");
```

## 🔁 OOPs Concepts in Dart

1. **Polymorphism** – Ability to take many forms (e.g., method overriding and method overloading but it does not support traditional method overloading).
2. **Abstraction** – Hiding implementation details and exposing only essential features.
3. **Inheritance** – Acquiring properties and behaviors from a parent class.
4. **Encapsulation** – Wrapping data and behavior into a single unit and restricting access.

---

## 🧱 Class in Dart

```dart
class Cookie {
  String shape = "Circle";
  double size = 15.2;

  Cookie(this.size, this.shape);

  void baking() {
    print("Baking a $shape cookie of size $size cm.");
  }
}
```

### Creating Object
```dart
Cookie cookie = Cookie(10.0, "Rectangle");
final cookie2 = Cookie(12.0, "Square");
cookie.shape = "Oval";
```

> `new` keyword is optional in Dart

---

## 🔒 Private Variables

- Use underscore `_` to make a variable **private**.
- Private in Dart means **file-private**, not class-private.

```dart
String _name = "Sachin";
```
## 🔒 Private Function
  void _privateFunction() {
    print("This is a private function.");
  }

---

## 📬 Getters and Setters

```dart
class Cookie {
  int _height = 0;

  // Getter
  int get height => _height;

  // Setter
  set setHeight(int h) {
    _height = h;
  }
}

cookie.setHeight = 15;
```

---

## Static Members

```dart
class Constants {
  static int value = 10;

  static int giveValue() {
    return value;
  }
}

Constants.value;
Constants.giveValue();
```

> Only static members can be accessed inside a static method.
>The static getter 'str' can't be accessed through an instance.

---

## 🧬 Inheritance

```dart
class Vehicle {
  int speed = 10;

  void accelerate() {
    speed += 10;
  }
}

class Car extends Vehicle {
  int noOfWheels = 4;

  @override
  void accelerate() {
    speed += 20;
  }
}

Vehicle myCar = Car();
(myCar as Car).noOfWheels;
```

> Dart does not support multiple inheritance but supports multilevel inheritance.

---

## Abstract Class & Implements

### Abstract Class

```dart
abstract class Vehicle {
  void accelerate(); // Abstract method
}
```

```dart
class Car implements Vehicle {
  @override
  void accelerate() {
    print("Car is accelerating...");
  }
}
```

> A class can `extend` one class and `implement` multiple interfaces.

```dart
class SportsCar extends BaseVehicle implements Drivable, Maintainable {
  @override
  void accelerate() {}

  @override
  void service() {}
}
```

---

## 🔁 Polymorphism Example

```dart
class Animal {
  void makeSound() {
    print("Animal sound");
  }
}

class Dog extends Animal {
  @override
  void makeSound() {
    print("Bark");
  }
}

class Cat extends Animal {
  @override
  void makeSound() {
    print("Meow");
  }
}

void main() {
  List<Animal> animals = [Dog(), Cat()];
  for (var animal in animals) {
    animal.makeSound();
  }
}
```

---

## 📦 Encapsulation Example

```dart
class BankAccount {
  double _balance = 0;

  double get balance => _balance;

  void deposit(double amount) {
    if (amount > 0) _balance += amount;
  }

  void withdraw(double amount) {
    if (amount > 0 && amount <= _balance) _balance -= amount;
  }
}
```

## 🔁 Mixins

- **Mixins** allow you to share functionality between classes without using inheritance.
- Use the `with` keyword to apply a mixin.
- Mixins **cannot be instantiated or extended**.

```dart
mixin Jump {
  int jumping = 10;
}

class Animal with Jump {
  void fn() {
    print(jumping);
  }
}
```

---

### 🚫 Using a Class as a Mixin (Incorrect)

> You **cannot use a regular class** as a mixin unless it's declared with `mixin` or `mixin class`.

```dart
class Animal {}

class Cat with Animal {} // ❌ Error
```

✅ **Correct (Dart 3+):**

```dart
mixin class Animal {}

class Cat with Animal {}
```

---

### 🔗 Multiple Mixins

- You can apply **multiple mixins** to a class.

```dart
mixin Jump {
  int jumping = 10;
}

mixin Scream {
  void scream() => print("Aaaah!");
}

class Animal with Jump, Scream {
  void fn() {
    print(jumping);
    scream();
  }
}
```

---

## 🧍‍♂️ Object Declaration

- The `Object` type can hold any value in Dart.

```dart
Object name = "Sachin";
```
Object name = "Sachin";

// This will give an error:
// print(name.toUpperCase()); ❌

print((name as String).toUpperCase()); // ✅ works after casting

---

## 🏷️ Class Modifiers

#### 🧪 Type Checking with `switch`

- Dart allows type checking using `switch` expressions (pattern matching style).

```dart
Animal animal = Cat();

switch (animal) {
  case Dog():
    print("Dog");
    break;
}
```

---

#### 🔧 `implements` Keyword

- Use `implements` to force a class to follow a certain structure.
- You must override **all members** of the interface.

```dart
class Animal {}

class Human implements Animal {
  // Must implement all members of Animal
}
```

---

###  `sealed` Classes (Dart 3+)

- A **sealed class** can only be extended or implemented in the same file where it is defined.
- All possible subclasses must be **exhaustively handled** in a `switch`.

```dart
sealed class Animal {}

class Dog implements Animal {}
class Human implements Animal {}

void checkAnimal(Animal animal) {
  switch (animal) {
    case Dog():
      print("Dog");
      break;
    case Human():
      print("Human");
      break;
  }
}
```

---

#### 🔐 `final` Classes

- A **final class** can be instantiated but **cannot be extended**.

```dart
final class Animal {}

final animal = Animal(); // ✅ Allowed

class Dog extends Animal {} // ❌ Error
```

---

#### 🧱 `base` Classes

- A **base class** can only be extended or implemented **within the same package**.
- It promotes better encapsulation.

```dart
base class Animal {}

class Dog extends Animal {} // ✅ Allowed within the same package
```


## 📦 List

An **ordered collection** of dynamic or specific type objects.

```dart
List list = [10, 20, 30, "Sachin"];         // dynamic list
Iterable list = [10, 20, 30, "Sachin"];     // also valid, more generic

print(list[0]);  // Output: 10
```

## 🧠 Generics in Classes

```dart
class Student<T> {
  T data;
  Student(this.data);
}

void main() {
  Student<String> student = Student<String>("Sachin");
  print(student.data);
}
```

Auto type checking ensures type safety at compile-time.

Check type at runtime:

```dart
if (student is Student) {
  print(student.data);
}
```

---

## 🔧 List Operations

```dart
List<int> list = [1, 2, 3];

// Access or update elements
list[2] = 30;

// Add elements
list.add(4);

// Insert at specific index
list.insert(1, 100);  // Push others ahead

// Remove by value
list.remove(3);

// Loop
for (final item in list) {
  print(item);
}

// Map
list.map((e) => print(e));

// Filter
list.where((item) => item >= 20).toList();

// Other useful methods
list.reversed.toList();
list.first;
list.last;
list.contains(30);
list.elementAt(2);
```

---

## 🎯 Sets

A **Set** is an unordered collection of unique items.

```dart
Set<Student> students = {
  Student("Ravaan", 10)
};
```

---

## 🗺️ Maps

A **Map** is a collection of key-value pairs. Each key is unique.

```dart
Map<String, int> marks = {
  "Ravaan": 10,
  "Navaan": 15,
  "Other": 30
};

print(marks["Ravaan"]);         // Output: 10
print(marks["name"]?.length);   // null safety
```

### 🔧 Map Operations

```dart
// Add multiple entries
marks.addAll({
  "John": 40,
  "Doe": 50
});

// Remove key
marks.remove("Other");

// Loop using index
for (int i = 0; i < marks.length; i++) {
  print(marks.keys.toList()[i]);
  print(marks.values.toList()[i]);
}

// Loop using forEach
marks.forEach((key, value) {
  print('$key: $value');
});
```

---

## 🧾 Enums

Use enums to define a fixed set of named constants.

```dart
enum EmployeeType {
  swe,
  finance,
  marketing
}
```

Use in class:

```dart
class Employee {
  final String name;
  final EmployeeType type;

  Employee(this.name, this.type);
}
```

---

## 🚀 Enhanced Enums

```dart
enum EmployeeType {
  finance(2000),
  marketing(2200);

  final int salary;
  const EmployeeType(this.salary);
}

void main() {
  EmployeeType emp = EmployeeType.finance;

  print(emp);             // Output: EmployeeType.finance
  print(emp.salary);      // Output: 2000
}

```

---

## ✅ Exception Handling
```dart
try {
  // code that might throw
} catch (e) {
  print("Caught error: $e");
} finally {
  print("Always executed");
}
```

OR for specific exceptions:
```dart
try {
  // risky code
} on FormatException catch (e) {
  print("Format Exception: $e");
} catch (e) {
  print("Other Exception: $e");
}
```

---

## ✅ Futures (like Promises in JavaScript)
```dart
Future<String> fetchData() async {
  return "Data loaded";
}

// OR

Future<String> fetchData() {
  return Future(() {
    return "Data loaded";
  });
}
```

### Delayed Response
```dart
Future<String> fetchLater() {
  return Future.delayed(Duration(seconds: 2), () {
    return "Data loaded";
  });
}
```

### Using `await`
```dart
void main() async {
  String data = await fetchData();
  print(data);
}
```

### Using `.then()`
```dart
void main() {
  fetchData().then((val) {
    print(val);
  }).catchError((e) {
    print("Error: $e");
  });
}
```

---

## ✅ `pub.dev` – Dart Package Repository
```dart
import 'package:http/http.dart' as http;
import 'dart:convert';

void main() async {
  final url = Uri.https("example.com", "/path");
  final res = await http.get(url);
  print(jsonEncode(res.body));
  print(jsonDecode(res.body));
}
```

---

## ✅ Streams
```dart
Stream<int> counter() async* {
  for (int i = 0; i < 3; i++) {
    yield i;
  }
}
```

### Listening to Stream
```dart
void main() async {
  await for (var val in counter()) {
    print(val);
  }
}

// OR

counter().listen((val) {
  print(val);
}, onDone: () {
  print("done");
});
```

### Periodic Stream
```dart
Stream<int> countDown() {
  return Stream.periodic(Duration(seconds: 1), (val) => val);
}
```

---

## ✅ StreamController
```dart
import 'dart:async';

void main() {
  final controller = StreamController<String>();

  controller.stream.listen(
    (data) => print('Received: $data'),
    onError: (error) => print('Error: $error'),
    onDone: () => print('Stream closed'),
  );

  controller.sink.add('Hello');
  controller.sink.add('World');

  controller.close();
}
```

---

## ✅ Records
```dart
final record = (4.5, "Hi", true, 2);
print(record.$1); // Access tuple items
```

### Named Record
```dart
final named = (4.5, text: "Hi", isAdult: true, 2);
print(named.text);
```

### Nullable
```dart
(double, int)? data = (2.0, 3);
print(data);
data = null;
print(data);
```

### Named destructuring
```dart
({int x, int y, int z}) point = (x: 1, y: 2, z: 3);
```

---

## ✅ Destructuring
### List
```dart
final list = [1, 2, 3];
final [a, b, c] = list;
```

### List with rest
```dart
final [a, b, c, ...rest] = [1, 2, 3, 4, 5];
```

### Map
```dart
final json = {
  "userId": 1,
  "id": 2,
  "title": "sunt",
  "body": "quia et"
};

final {"userId": userId, "title": title} = json;
```

### Using `case`
```dart
if (json case {"userId": int userId, "title": String title}) {
  print("$userId - $title");
}
```

---

## ✅ Destructuring Class Fields
```dart
class Human {
  final String name;
  final int age;
  Human(this.name, this.age);
}

final human = Human("Nice Name", 2);

final Human(:name, :age) = human;
print(name);
```

---

## ✅ Pattern Matching (Dart 3)
```dart
List<String> listItem = ["HI", "MAN"];

switch (listItem) {
  case ["Hi" || "HI", "MAN"]:
    print("Dude!");
    break;
}

final text = switch (page) {
  0 => "Click",
  1 when page == lastPage => "Last Page",
  _ => "Default"
};
```

---

## ✅ Extensions
```dart
extension CapitalizeFirst on String {
  String capitalizeFirstLetter() {
    return this[0].toUpperCase() + substring(1);
  }
}

void main() {
  String name = "sachin";
  print(name.capitalizeFirstLetter());
}
```

__________________________  complete Dart _______________________________