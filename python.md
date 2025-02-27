#                                    Python 3.11

### why?
Easy to read and learn
Various existign libraries and frameworks
large community and documention 
automate our day to day task
can create GUI based , website and games

.py file

### run file 
--> phython3 filename.py

### print 
```py
print()
print(f"sum of two numbers are {10+20}")
```
here f --> formating

### comments
use #
and use for multiple lines use """ or '''
"""   """
'''   '''

### Variables
name = "sachin"
length =20

--> rules to define variables
* should not start with number
* no spaces
* no special character
* not use build-in name

bol=True / False (bool)
average=45.5 float
number =10 (int)
name ="sachin"  (str)

--> stringly typed language 
do not allow 
type casting

### check type 
type(variable_name)

--> calculate powers
2**5
10/3 --> 3.333
10//3 -> 3

### Strings
string are immutable
we can use "" ''
use + to ass two strings

.lower()
.upper()
.title() make first word in sentence capital
.split()

strigns are iterable
str[0]
str[0:5] --> range 
-1 from last

### Explicit type conversion
-> Convert int to float
num = 10
print(float(num))  # Output: 10.0

-> Convert float to int (loses decimal part)
pi = 3.14
print(int(pi))  # Output: 3

-> Convert int to string
num = 100
print(str(num))  # Output: "100"

-> Convert string to int (if valid)
s = "50"
print(int(s))  # Output: 50

int(x)	Integer
float(x)	Float
str(x)	String
bool(x)	Boolean
list(x)	List
tuple(x)	Tuple
set(x)	Set

(int → float → complex)

In Python, the complex data type is used to represent complex numbers. A complex number consists of a real part and an imaginary part.
The imaginary part must have j or J (Python uses j instead of i like in mathematics).

c = complex(5, -3)  
print(c)        # Output: (5-3j)
print(type(c))  # Output: <class 'complex'>

### Lists in python
Ordered Sequence of different types of values
users=["a",1,"10"]
users[0]

.append("paul") --> add  in end
.pop()
.remove("sachin") -> will remove this
insert()
.clear()
.cop()

✔ append(x) → Adds x to the end of the list.
✔ pop([i]) → Removes and returns the last item (or item at index i).
✔ remove(x) → Removes first occurrence of x. will throgh error when value not in list
✔ insert(i, x) → Inserts x at index i.
✔ clear() → Removes all elements from the list.
✔ copy() → Returns a shallow copy of the list.
✔ del list[3] -> will delete value at 3
✔ len(list) -> give list length
✔  sort(list)  .sort(reverse=True)

slicing in list
list[0:5]
list[:5]
list[-2:]

--> if list contains numbers
min(list)
max(list)
sum(list)

### Tuples
sames as list, however we can;t modify the items of tuple

immutable , ordered

days=("mon","tues")
days[0]
days.count("mon") -> return number of occurance
days.index("tue") -> give index of value

# Dictionaries
key:value









