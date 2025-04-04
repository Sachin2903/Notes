#                                                Dart
--> Dart is developed by google
is is an combination of  javascript and java , python

#### Compilaation process
Dart use 2 compilation proccess 
 converting source code to machine code

> JIT
Fast iteration and immediate feedback

> AOT
compile the dart code in optimise way making application efficient for use

> Dart is a typed language
#### SDK 
Software development kit :- tools require for system to understand DART

so we  can use
--> flutter SDK contain Dart SDK ( for dark )
or 
--> Dart SDK ( only for dark code )
--> Dart Pad ( help us to write dart in browser itself , its an online compiler to dark )

```dart
void main() {
  for (var i = 0; i < 10; i++) {
    print('hello ${i + 1}');
  }
}
```
* need to ha ;

### Print
prin()
print("helloe world"+2); --> not allowed
print("helloe world"*2); --> this print this twice in a same line

### Comments
// single line comments
/*
multi line comments
*/

### Variable

* Integer
int 
eg:- int firstValue=3;
firstValue.isEven
firstValue.isOdd

* String
String
eg: String str="sachin"
str.length
str[i]

* Boolean
bool check=true,false;

* dynamic
dynamic variable =18.8;
dynamic.runtimeType

### Increment and decrement operator
++, --;

### String interpulation
`${}`

use \ to remove the impotance
`\$2`

### this to make a string like textbox
"""    """"
\n for next line

### var , final , const
var ="string", 10
this evaluate the type from right side my own

final someValue=10;
const someValue=10;

DateTime.now()

final a = [1, 2, 3]; // New list at runtime
final b = [1, 2, 3]; // Another new list

const c = [1, 2, 3]; // Compile-time constant
const d = [1, 2, 3]; // Reuses same object as 'c'

print(identical(c, d)); // true
print(identical(a, b)); // false

✅ No — your logic will be the same.
⚠️ But your app may be slower or use more memory if you don’t use const where possible.

final String str="sachin";
  print(str);
const  String str="sachin";
  print(str);

### optional variable
String some=null; // this was allowed in below dart 2
String? str=null; // this is in dart 2 and above
String? str;

str?.length
 
(null ?? 0) 

### if and else, else if statement

if(age>=10){
    print()
}else{
    print()
}

else if 

### Operator
=,==
&& , ! 

an integer could not be a truly or falsy value untill it combine with operators

> String function
.isEmpty()
.isNotEMpty()
.startsWith()
.substring(1,3)

### Switch
switch(){
    case "":
    print(")
    default :
}

don not need to use break . only have to use break if the statement is empty

case "hi":
break;

switch didn;t allow using relational operators like ==,!= until dart 3

case "Hi" when age>=23

## Loops
for (init i=0;i<=10;i++){
    
}

while(){

}

do{

}while()

break; continue;

### Function






































