# Python 3.11

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

-> Convert string to i




nt (if valid)
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
remove can't be empty and can not have value that is not present in the list
insert()
.clear()
.cop()

✔ append(x) → Adds x to the end of the list.
✔ pop([i]) → Removes and returns the last item (or item at index i).
✔ remove(x) → Removes first occurrence of x. will throgh error when value not in list
✔ insert(i, x) → Inserts x at index i.
✔ clear() → Removes all elements from the list.
✔ copy() → Returns a shallow copy of the list.
✔ del list[3] -> will delete value at 3, can not be out of range
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

### Dictionaries
key:value

marks={ "Hindi":80 }
print(marks)
marks["Hindi"]

marks.get("Hindi")
this is better to avoid error if any error is not in the dictionary

del marks["hindi"]

len(marks)

### Sets
my_sets={"mon","tue"}
onyl store unique value and unorder value

my_sets.add("fri")
my_sets.pop()


my_list=["mon","tues"];
days_set=set(my_list)
print(days_set)

### user inteaction
name =input("whats's you name")
age=int(input("your age"))

### COnditional statement

if age>=18:
 print(" aligible to vote")
else:
 print("not aligible to vote")

users=["paul,"raju"]
if "paul' in users:
print("")

if 15<52:
elif 10>12:
else:

### LOgical operator

and , or 

10<20 and 20<50
10>20 or 10<20

### Loops
for i in 1,2,3,5,5:
print(i)

--> in list
num=[1,2,3,4,5,6]
for i in num:
print(i)

--> in dictionaries
age_info={raju:25,sham:30}
for name, age in age_info.item()

for name in age_info.keys()
for age in age_info.values()

for num in range(1,10)
print(num)
1-9

### while loop
while 10>20:
prin("while loop")

### break and continue
break
continue

### Functions
def myFUn():

myfun()

def myFUn(a,*b)

b wiill contain all remaing parameters as a list
print("*"*20)
this will print * 20 times

**user_info now things will be in dictionaries

myfunction(age=18,city="delhi")

### function as module
import calcy (filename)

calcy.add()
add will be the function written in calcy.py file

### OOPS
class and object

class -->
```py
class Employees:
    company="abc.p vt"
    def __init__(self,name ,dept):
self.name=name
self.dept=dept

def classFUn(self):



# object -->
emp1=Employees("rangu","sales");
emp1.salary

Employees.company
# can also directly accessible
pass
```

use class in another file

import filename

employess.EMployess()

# Exception Handling
```py
try:
print(10/0)
except ZeroDivisionError:
    print("try error name ,can get this error name from console terminal")

try:
print(10/0)
except Exception as e:
    print("try error name ,can get this error name from console terminal")
finally:
    
```
## random and datetime

import random
random.random()
regenrate a random float between 0 to 1
random.random(1,100)
regenrate a random float between 1 to 100

options=["apple"]
random.choice(options)


