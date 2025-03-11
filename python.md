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

### Exception Handling
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
### random and datetime

import random
random.random()
regenrate a random float between 0 to 1
random.random(1,100)
regenrate a random float between 1 to 100

options=["apple"]
random.choice(options)


# Django
You can refer to [W3Schools Django Tutorial](https://www.w3schools.com/django/)


* Django is python web framework
* Django is backend server side web framework
* Django makes easier to build web pages using python 
Take cares of difficult stiff so that we can concentrate on building web apps.
* provides amny built in features.

Django follows MVT design pattern
Model -data we want to present , usually data from a database.

View - A request handler that returns the relevant template and content - based on the request from the user.

Template - a text file containing the layout of the wen page,with logic on how to display the data

user <---> Django <--> URL <---> View <----> Model
                                  |
                                  |
                               Template


sudo apt install python3-pip
* PIP :- pip is the package manager for Python. It is used to install, update, and manage Python packages from the Python Package Index (PyPI).

>> sudo apt install python3 python3-venv python3-pip

##### virtaul environment in python ( for same system environment )
Install Django
pip install django
pip install django==3.0.2

Verify Django Installation
django-admin --version

django-admin startproject myproject
cd myproject
python manage.py runserver


###### project based virtual env
cd path/to/your_project
python -m venv venv
venv\Scripts\activate or in linux source venv/bin/activate

pip install django
django-admin startproject myproject .
pip freeze > requirements.txt
deactivate

pip freeze → Lists all installed packages and their versions.
> requirements.txt → Redirects (>) the output to a file (requirements.txt).



pip install -r requirements.txt
tells pip to read the list of packages from the specified file (requirements.txt) and install them.

📌 Advantages of a Project-Based Virtual Environment
✅ Keeps dependencies isolated for each project.
✅ Avoids conflicts between different Django projects.
✅ Easy to share using requirements.txt.
✅ Ensures smooth deployment in production.

#### file structure
project2/                # Project root directory
│── manage.py            # Command-line utility for Django
│── project2/            # Inner directory (project package)
│   │── __init__.py      # Marks this as a Python package
│   │── settings.py      # Main configuration file
│   │── urls.py          # URL routing for the project
│   │── asgi.py          # ASGI entry point (for async servers)
│   └── wsgi.py          # WSGI entry point (for web servers)

📌 How These Files Work Together
* manage.py runs Django commands like starting the server or making migrations. and help us to communicate with the project
* settings.py configures the project (database, static files, apps, etc.).
* urls.py defines the URL patterns that direct user requests.
* asgi.py and wsgi.py are used when deploying Django apps.

--> start the development server
>> python3 manage.py runserver
--> specify specific ip and port
>> python3 manage.py runserver 127.0.0.1:9090

##### import a file
```py
from app.models.user import User  # Import User class from nested folder
from .views import *
```

```py
# in urls.py
from .views import *
path('index/', test),

# in view.py

from django.http import HttpResponse
import datetime
def test(request):
print("test function is called from view")
datetime.datetime .now()
return HttpResponse("<h1>Hello thi si index page</h1>")

```

django is composed of apps
--> create a new app inside same project
>> python manage.py startapp website

once create app add them settings.py of main app
INSTALLED_APPS=[
   "website",
   "apis" 
]

#### template
./Templates
about.html

style="text-align:center"
html boiler plate

go in settings telss where the temmplate were store

import os
TEMPLATES=[
    {
        DIRS:[os.path.join(BASE_DIR,"templates")]
    }
]
```py
from django.shortcuts import render
return render(request,"home.html",{})
```

--> to include one html into another
{% include `navbar.html` %}

--> pass data from view to html
 {{date}}

 { % if isActive % }
 { % endif %}

 { % for i in list % }
 { % endfor %}

--> data from url or user

<form action="/index" method="POST">
{% csrf_token %}
<input type="text" name="check">
<button>Send</button>
</form>

```py
   if request.method=="POST"
   check=request.POST["check"]
   print(check)
```

#### Models
model.py

python manage.py makemigrations
This creates a migration file inside the migrations/ folder of your Django app, e.g.

python manage.py migrate

* Scans all apps listed in INSTALLED_APPS inside settings.py
* Detects changes in all models.py files
* Creates migration files for each app separately


💡 What If You Want to Create Migrations for Only One App?

python manage.py makemigrations app1
This will only generate migrations for app1 and ignore others.

 After makemigrations, you must run migrate to apply changes to the database
✔ Run it every time you modify models.py to keep the database schema updated

```py
# in models.py

from django.db import models
class Student(models.Model):
    name=models.CharField(max_length=200,default="Unknown Student")
    college=models.CharField(max_length=200)
    age=models.IntegerField(max_length=200)
    is_active=models.BooleanField(default=False)
    testimonial=models.TextField()
    picture=models.ImageField(upload_to="testtimonials")
          

```

--> det default value 
```py
from django.db import models

def get_default_college():
    return "Not Assigned"

class Student(models.Model):
default=get_default_college)

 created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True) 
```


######  Meta
The Meta class in Django models provides metadata for the model, controlling various behaviors like sorting, database constraints, permissions, and more.

```py
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=200)
    age = models.IntegerField()
    roll_number = models.CharField(max_length=20, unique=True)
    admission_date = models.DateField(auto_now_add=True)

    class Meta:
        ordering = ['name']  # Default sorting by name
        verbose_name = "Pupil"  # Singular name in admin panel
        verbose_name_plural = "Pupils"  # Plural name in admin panel
        db_table = "student_info"  # Custom database table name
        unique_together = ('name', 'roll_number')  # Ensures name & roll_number combination is unique
        index_together = [('name', 'age')]  # Creates an index for faster queries on name & age
        default_permissions = ('add', 'change', 'delete')  # Default permissions
```

__str__ defines how an object is displayed as a string.
```py
class Student(models.Model):
    name = models.CharField(max_length=200)

    def __str__(self):
        return self.name
```
🔹 Without __str__ → <Student: Student object (1)>
🔹 With __str__ → "John" 🚀


__str__()	Defines how an object is displayed as a string
__repr__()	Debugging representation
save()	Custom logic before saving an object
delete()	Custom logic before deleting an object
get_absolute_url()	Generates a URL for the object
__eq__()	Custom comparison of objects



--> to directly compunicate with terminal 

python3 ./manage.py shell






students.object.get()
students.object.get(id=1)
students.object.all()

https://docs.djangoproject.com/en/5.1/topics/db/queries/

2 projects myapp and emp
in myapp url.py

```py
from django.urls import path,include
urlpattterns=[
    path("admin/",include('emp.urls'))
]
```

in emp app
in url.py
```py
urlpattterns=[
    path("admin/",include('emp.urls'))
]
```
```py
from django.shortcuts import render,redirect
def emp_home(request):
if(true)
redirect("/pu")
return render(request,"emp/home.html",{})
```

```py
from .model import Emp;

e=Emp();
e.name="sachin"
e.email="sachin1234@gmail.com"
```

if e is None 

emps=Emp.Objects.all()

path("delete-emp/<int:emp_id>",add_emp)
path("delete-emp/<int:emp_id>/<str:dept>", add_emp)
from django.http import JsonResponse
def add_emp(request, emp_id, dept):
    return JsonResponse({"emp_id": emp_id, "dept": dept})


def delete_emp(request,emo_id){
    print(emp_id)
redirect("/emp/home")
}

emp=Emp.objects.get(pk=emp_id)
emp.delete()


##### query

http://127.0.0.1:8000/delete-emp/5/HR/?status=active&page=2
def add_emp(request, emp_id, dept):
    status = request.GET.get("status", "default_value")
    page = request.GET.get("page", 1)  # default to 1 if not provided

    return JsonResponse({
        "emp_id": emp_id,
        "dept": dept,
        "status": status,
        "page": page
    })


##### can use regex in url 
from django.urls import re_path

urlpatterns = [
    re_path(r"^delete-emp/(?P<emp_id>\d+)/(?P<dept>\w+)/?$", add_emp),
]

## Admin and admin customization
/admin

--> to create username and password


pthon3 manage.py createsuperuser
set name , email , password


--> this allow CRUD operations in admin panel

admin.py
```py
from django.cortrib import admin
from .models import Emp

admin.site.register(Emp)

```

--> show table in admin panel
class EmpAdmin(admin.ModelAdmin):
list_display=("name","working","emp_id")
list_editable=("working")
search_fields=("name","phone")
list_filter=("working")
admin.site.register(Emp,EmpAdmin)


##### Media in python

in setting.py
MEDIA_URL="/media/"
MEDIA_ROOT=os.path.join(BASE_DIR,"media")
 

 url.py
from django.conf import settings
from django.conf.urls.static import static

 ]+static(settings.MEDIA_URL,document_root=settings.MEDIA_ROOT)

 ##### Forms class
 form.py
 
 ```py
from django import forms

class FeedbackForm(forms.Form):
    email=forms.EmailFields(label="email label",max_length=100)
    name=forms.CharFIeld(label="Enter you name",max_length=100)



 ```

 view.py
 ```py
from .form import FeedbackFrom
 if(request.method=="POST")
 pass
 else:
form=FeedbackForm()
return render(request,"emp/feedback.html",{"form":form})
```

<form action="">
{{form}}
</form>

form.as_table
form.as_p
form.as_ul


add class in class form
 ```py
from django import forms

class FeedbackForm(forms.Form):
    email=forms.EmailFields(label="email label",max_length=100)
    name=forms.CharFIeld(label="Enter you name",max_length=100)

def __init__(self,*args,**kwargs):
    super(FeedbackForm,self).__init__(*args,**kwargs)
    for visible in self.visible_fields():
        visible.fields.widget.atts["class"]="form-control"

 ```