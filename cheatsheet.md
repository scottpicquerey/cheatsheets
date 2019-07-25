# Python cheatsheet

## If conditions

```python
a = 4
b = False
c = [1, 2, 3 , 4]

if a > 1 and a < 7: # or
    print("Value {} is in range 2 -> 6".format(a))

if b is not True:
    print("Value {} is not True".format(b))

if a in c:
    print("Value {} is in list {}".format(a, c))
```

## Inputs

```python
nom = input("Quel est votre nom") # always returns a string
```

## For loops

```python
a = [1, 2, 3, 4]

for item in a:
    print(item)

for i, item in enumerate(a):
    print("{}: {}".format(i, item))

for item in a:
    print(item)
    if item == 2:
        break;

for item in a:
    if item == 2:
        continue;
    print(item)

# For dictionnaries
fruits = {
    "apple": 4,
    "banana": 6
}

for fruit in fruits:
    print(fruit)

for fruit in fruits.keys(): # Same result as above
    print(fruit)

for value in fruits.values():
    print(value)

for key, value in fruits.items():
    print("{} {}".format(key, value))
```

## While loops

```python
a = [1, 2, 3, 4]

while len(a) > 0:
    del a[0]

print(a)
```

## Functions
```python
def my_function(param1, param2="toto"): # toto by default
    return param1, param2

my_lambda_fct1 = lambda x: x*x
my_lambda_fct2 = lambda x, y: x*y
```

## Modules
```python
import math # If need help : help(math) or help(math.sqrt)

import math as mathematiques

from math import sqrt
from math import *

from my_file import my_function
```

## Exceptions

https://docs.python.org/3/library/exceptions.html

```python
try:
    print("Hello")
except:
    print("Error")
    pass # If no action is done in except
else:
    print("No errors in the try")
finally:
    print("Printed anyways")

try:
    raise ValueError("A value error")
except ValueError:
    print("Value error")
except:
    print("Error")
```

## Assertions

Check if a condition is True

```python
a = 5

assert a == 5 # True so nothing happens
assert a == 7 # False -> raise error
```

## Print

```python
prenom = "Scott"
nom = "Picquerey"
age = 25

# Mettre des variables dans un string
print("Je m'appelle {} {} et j'ai {} ans".format(prenom, nom, age))
print("Je m'appelle {0} {1} et j'ai {2} ans".format(prenom, nom, age))
print("Je m'appelle {0} {1} et j'ai {2} ans. Je suis {0}".format(prenom, nom, age))
print("""Je m'appelle {prenom} {nom} et j'ai {age} ans""".format(prenom="toto", nom=nom, age=age))
```

## String

```python
phrase = "hello "

phrase.lower() # lowercase
phrase.capitalize() # first letter uppercase, rest lowercase
phrase.upper() # uppercase
phrase2.strip() # remove spaces at start & end of string
phrase2.upper().strip()

prenom = "scott"
nom = "picquerey"
age = 25

info = prenom + " " + nom + " " + str(age)
info_array = info.split(" ") # returns array with 3 items
```

## Arrays

```python
my_array = [1, 2, 3]

my_array.append(4)
my_array.insert(1, 1.5)

my_array_combinaison = my_array + my_array # [1, 2, 3, 1, 2, 3]

del my_array[1] # remove by index position
my_array.remove(3) # remove by value

string_joined_array = " ".join(my_array)
```

## Dictionnaries

Nb: It is possible to store functions in dictionnaries.

```python
my_dict = {
    "key": "value"
}

my_other_dict = {}
my_other_dict[0] = "toto" # {0: "toto"}

del my_dict["key"]
value_of_key = my_dict.pop("key") # del key and returns its value

my_dict["stored_function"]("param1")
```

## Files

Classic way

```python
my_file = open("my_file.txt", "w") # w: write, r: read, a: append, wb: write binary
my_file.write("hello")
my_file.close()

my_file = open("my_file.txt", "r")
print(my_file.read())
my_file.close()

my_file = open("my_file.txt", "a")
my_file.write("hello")
my_file.close()

with open("my_file.txt", "r") as my_file:
    text = my_file.read()
    print(text)
```

Using pickle

```python
import pickle

score = {
    "scott": 10
}

with open("my_pickle", "wb") as my_file:
    my_pickle = pickle.Pickler(my_file)
    my_pickle.dump(score)

with open("my_pickle", "rb") as my_file:
    my_pickle = pickle.Unpickler(my_file)
    print(my_pickle.load())
```

## Classes

```python
class Person:
    counter = 0

    def __init__(self, name): # Constructor; self ~= this in JS
        Person.counter += 1
        self.name = name
        self.description = ""
        self._residence = "Paris" # _ means that residence (not _residence) is not accessible from outside of the class. We use setters / getters
    
    def decription_update(self, msg):
        self.description = msg
    
    def _get_residence(self):
        return self._residence

    def _set_residence(self, new_residence):
        self._residence = new_residence
    
    residence = property(_get_residence, _set_residence)

    def static_method():
        print("Hello!")
    static_method = staticmethod(static_method)

    def __del__(self): # Destructor
        print("Class instance deleted")

person_instance = Person("Scott")
print(person_instance.name)

other_person = Person("Jack")
print(Person.counter) # 2

Person.static_method()

print(person_instance.residence)
person_instance.residence = "Lyon"
print(person_instance.residence) # Lyon
```

## Inheritance

```python
class Person:
    def __init__(self, name):
        self.name = name

    def say_my_name(self):
        print(self.name)

class Engineer(Person):
    def __init__(self, name, company):
        self.name = name
        self.company = company
    
    def __str__(self):
        return "{}, engineer at {}".format(self.name, self.company)

engineer = Engineer("Scott", "IBM")
print(engineer)
engineer.say_my_name()
```

## Sorting

Sort array & dictionnary

```python
from operator import itemgetter

my_array = [2, 3, 1, 5]

my_dict = {
    "apple": 10,
    "peach": 3,
    "banana": 7
}

print(sorted(my_array))
print(sorted(my_array, reverse=True))

print(sorted(my_dict)) # sort by key name
print(sorted(my_dict, key=itemgetter(2))) # sort by value
print(sorted(my_dict, key=itemgetter(2), reverse=True)) # sort by value
```

## Decorators

```python
def my_decorator(function):
    print("The decorator is called!")
    return function

@my_decorator
def my_function():
    print("Function called")

my_function() # decorator is called before executing the function
```