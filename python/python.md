## Data Structures
### Data Structures 1 - Lists
```python
letters = ["a", "b", "c"]
print(letters)

matrix = [[0, 1], [2, 3]]
print(matrix)

zeros = [0] * 5
print(zeros)

combined = zeros + letters
print(combined)

numbers = list(range(20))
print(numbers)

chars = list("Hello World")
print(chars)
```
```output
['a', 'b', 'c']
[[0, 1], [2, 3]]
[0, 0, 0, 0, 0]
[0, 0, 0, 0, 0, 'a', 'b', 'c']
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
['H', 'e', 'l', 'l', 'o', ' ', 'W', 'o', 'r', 'l', 'd']
```

### Data Structures 2 - Accessing Items
```python
letters = ["a", "b", "c", "d"]
print(f"letters[1] = {letters[1]}")
print(f"letters[-1] = {letters[-1]}")
print(f"letters[0:3] = {letters[0:3]}")
print(f"letters[:3] = {letters[:3]}")
print(f"letters[0:] = {letters[0:]}")
print(f"letters[:] = {letters[:]}")
print(f"letters[::] = {letters[::]}")
numbers = list(range(10))
print(f"numbers[::2] = {numbers[::2]}")
print(f"numbers[::3] = {numbers[::3]}")
print(f"numbers[::-1] = {numbers[::-1]}")
```
```output
letters[1] = b
letters[-1] = d
letters[0:3] = ['a', 'b', 'c']
letters[:3] = ['a', 'b', 'c']
letters[0:] = ['a', 'b', 'c', 'd']
letters[:] = ['a', 'b', 'c', 'd']
letters[::] = ['a', 'b', 'c', 'd']
numbers[::2] = [0, 2, 4, 6, 8]
numbers[::3] = [0, 3, 6, 9]
numbers[::-1] = [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

### Data Structures 3 - List Unpacking

```python
numbers = list(range(10))
first, second, third, *other, last = numbers
print(first, last)
print(second)
print(third)
print(other)


# Use * to pack the input args into list
def print_list(*numbers):
    for number in numbers:
        print(number)

print_list(1, 2, 3, 4, 5)
```
```output
0 9
1
2
[3, 4, 5, 6, 7, 8]
1
2
3
4
5
````

### Data Structures 4 - Looping over Lists

```python
letters = ["a", "b", "c"]
for letter in enumerate(letters):
    print(letter)

# Unpacking
for index, value in enumerate(letters):
    print(index, value)
```
```output
(0, 'a')
(1, 'b')
(2, 'c')
0 a
1 b
2 c
```

### Data Structures 5 - Adding or Removing Items

```python
letters = ["a", "b", "c"]

# Add
letters.append("d")
letters.insert(0, "-")
print(letters)

# Remove
letters.pop()
print(letters)
letters.pop(0)
print(letters)
letters.remove("b")
print(letters)

numbers = list(range(10))
del numbers[0:3]
print(numbers)
numbers.clear()
print(numbers)
```
```output
['-', 'a', 'b', 'c', 'd']
['-', 'a', 'b', 'c']
['a', 'b', 'c']
['a', 'c']
[3, 4, 5, 6, 7, 8, 9]
[]
```

### Data Structures 6 - Finding Items

```python
letters = ["a", "b", "c"]
print(letters.index("a"))
if "d" in letters:
    print(letters.index("d"))
print(letters.count("a"))
print(letters.count("d"))
```
```output
0
1
0
```

### Data Structures 7 - Sorting Lists

```python
numbers = [3, 51, 2, 8, 6]
numbers.sort(reverse=True)
print(numbers)
# print(sorted(numbers, reverse=True))
print(sorted(numbers))
print(numbers)
````
```output
[51, 8, 6, 3, 2]
[2, 3, 6, 8, 51]
[51, 8, 6, 3, 2]
```

```python
items = [
    ("product1", 10),
    ("product2", 9),
    ("product3", 12),
]
items.sort()
print(items) # Nothing happen

def sort_item(item):
    return item[1]

items.sort(key=sort_item)
print(items) # Nothing happen
```
```output
[('product1', 10), ('product2', 9), ('product3', 12)]
[('product2', 9), ('product1', 10), ('product3', 12)]
```

### Data Structures 8 - Lambda Functions

```python
items = [
    ("product1", 10),
    ("product2", 9),
    ("product3", 12),
]

items.sort(key=lambda item:item[1])
print(items)
```

### Data Structures 9 - Map Function

```python
items = [
    ("product1", 10),
    ("product2", 9),
    ("product3", 12),
]

prices = list(map(lambda item: item[1], items))
print(prices)
```
```output
[10, 9, 12]
```

### Data Structures 10 - Filter Function

```python
items = [
    ("product1", 10),
    ("product2", 9),
    ("product3", 12),
]

x = list(filter(lambda item: item[1] >= 10, items))
print(x)
```

### Data Structures 11 - List Comprehensions

```python
items = [
    ("product1", 10),
    ("product2", 9),
    ("product3", 12),
]
prices_a = list(map(lambda item: item[1], items))
prices_b = [item[1] for item in items] # Recommended

print(prices_a)
print(prices_b)

filtered_a = list(filter(lambda item: item[1] >= 10, items))
filtered_b = [item for item in items if item[1] >= 10] # Recommended

print(filtered_a)
print(filtered_b)
```
```output
[10, 9, 12]
[10, 9, 12]
[('product1', 10), ('product3', 12)]
[('product1', 10), ('product3', 12)]
```

### Data Structures 12 - Zip Function

```python
list1 = [1, 2, 3]
list2 = [10, 20, 30]

print(list(zip("abc", list1, list2)))
```
```output
[('a', 1, 10), ('b', 2, 20), ('c', 3, 30)]
```

### Data Structures 13 - Stacks

```python
browsing_session = []
browsing_session.append(1)
browsing_session.append(2)
browsing_session.append(3)
print(browsing_session)
print(browsing_session.pop())
print(browsing_session[-1])
print(browsing_session.pop())
if not browsing_session:
    print(browsing_session[-1])

```
```output
[1, 2, 3]
3
2
2
```

### Data Structures 14 - Queues

```python
from collections import deque

queue = deque([])
queue.append(1)
queue.append(2)
queue.append(3)
print(queue.popleft())
print(queue)
if not queue:
    print("Empty")
```
1
deque([2, 3])
```


### Data Structures 15 - Tuples

```python
point = 1, 2
print(type(point))
```
```python
<class 'tuple'>
<class 'tuple'>
(6, 7, 6, 7, 6, 7)
('H', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd', '!')
```

### Data Structures 16 - Swapping Variables

```python
x = 6
y = 7

x, y = y, x
print("x", x)
print("y", y)
```

### Data Structures 17 - Arrays

***Don't solve a problem doesn't exist!***

```python
from array import array

numbers = array("i", [1, 2, 3])
numbers.append(4)
print(numbers)
numbers.insert(2, 2)
print(numbers)
# numbers.remove(0)
```
```output
array('i', [1, 2, 3, 4])
array('i', [1, 2, 2, 3, 4])
```

### Data Structures 18 - Sets

```python
numbers = [1, 1, 2, 3, 3, 4]
first =set(numbers)
second = {1, 3}
second.add(5)

print(first | second)
print(first & second)
print(first - second)
print(first ^ second)

if 1 in first:
    print("Yes")
```
```output
{1, 2, 3, 4, 5}
{1, 3}
{2, 4}
{2, 4, 5}
Yes
```

### Data Structures 19 - Dictionaries

```python
point = {"x": 1, "y": 2}
point = dict(x=1, y=2, z=3)

if "a" in point:
    print(point["a"])
else:
    print(point.get(("a", 0)))

del point["x"]
print(point)

for k, v in point:
    print(k)
    print(v)
    print((k, v))
```

### Data Structures 20 - Dictionary Comprehensions

```python
# values = []
# for x in range(5):
#     values.append(x * 2)

values = [x * 2 for x in range(5)]
print(values)

dicts = {x: 'value as ' + str(x*2) for x in range(5)}
print(dicts)
```
```output
[0, 2, 4, 6, 8]
{0: 'value as 0', 1: 'value as 2', 2: 'value as 4', 3: 'value as 6', 4: 'value as 8'}
```

### Data Structures 21 - Generator Expressions

```python
from sys import getsizeof

values = (x * 2 for x in range(5))
print(values)
for x in values:
    print(x)

big_values = (x * 2 for x in range(100000000))
print("gen: ", getsizeof(big_values))

big_values = [x * 2 for x in range(1000000)]
print("list: ", getsizeof(big_values))
```
```output
<generator object <genexpr> at 0x7f890875fac0>
0
2
4
6
8
gen:  112
list:  8697456
```

### Data Structures 22 - Unpacking Operator

```python
numbers = [1, 2, 3]
print(numbers)
print(*numbers)
print(1, 2, 3)
```
```output
[1, 2, 3]
1 2 3
1 2 3
```

```python
values = list(range(5))
print(values)
values = [*range(5), *"Hello"]
print(values)
```
```output
[0, 1, 2, 3, 4]
[0, 1, 2, 3, 4, 'H', 'e', 'l', 'l', 'o']
```

```python
first = [1, 2]
second = [3]

values = [*first, "a", *second, *"Hello"]
print(values)
```
```output
[1, 2, 'a', 3, 'H', 'e', 'l', 'l', 'o']
```

```python
first = {"x": 1}
second = {"x": 10, "y": 2}
combined = {**first, **second, "z": 1}
print(combined)
```
```output
{'x': 10, 'y': 2, 'z': 1}
```

### Data Structures 23 - Exercise

```python
from pprint import pprint

sentence = "This is a common interview question"

char_freq = {}

for char in sentence:
    if char in char_freq:
        char_freq[char] += 1
    else:
        char_freq[char] = 1

pprint(char_freq, width=1)

char_freq_sorted = sorted(
    char_freq.items(), 
    key=lambda kv: kv[1],
    reverse=True)
print(char_freq_sorted)
print(char_freq_sorted[0])
```

## Exceptions
### Exceptions 1 - Exceptions

```python
numbers = [1, 2]
print(numbers[3])
```
```output
Traceback (most recent call last):
  File "/Users/mac/PycharmProjects/demo/main.py", line 2, in <module>
    print(numbers[3])
IndexError: list index out of range
```

```python
age = int(input("Age: "))
```
```sh
python main.py 
```
```output
Age: a
Traceback (most recent call last):
  File "main.py", line 1, in <module>
    age = int(input("Age: "))
ValueError: invalid literal for int() with base 10: 'a'
```

### Exceptions 2 - Handling Exceptions

```python
try:
    age = int(input("Age: "))
except ValueError as e:
    print("You didn't input a valid age.")
    print(e)
    print(type(e))
else:
    print("No exceptions were thrown.")
print("Execution continues.")
```
```sh
python main.py
`=>
Age: a
You didn't input a valid age.
invalid literal for int() with base 10: 'a'
<class 'ValueError'>
Execution continues.
```

### Exceptions 3 - Handling Different Exceptions

```python
try:
    age = int(input("Age: "))
    xfactor = 10 / age
except (ValueError, ZeroDivisionError):
    print("You didn't input a valid age.")
# except ZeroDivisionError:
#     print("You didn't input a valid age.")
else:
    print("No exceptions were thrown.")
```

### Exceptions 4 - Cleaning Up

*Bad implementation with duplication*
```python
try:
    file = open("main.py")
    age = int(input("Age: "))
    xfactor = 10 / age

except (ValueError, ZeroDivisionError):
    file.close()
    print("You didn't input a valid age.")
# except ZeroDivisionError:
#     print("You didn't input a valid age.")
else:
    file.close()
    print("No exceptions were thrown.")
```

```python
try:
    file = open("main.py")
    age = int(input("Age: "))
    xfactor = 10 / age
except (ValueError, ZeroDivisionError):
    print("You didn't input a valid age.")
else:
    print("No exceptions were thrown.")
finally:
    file.close()
```

### Exceptions 5 - The With Statement

```python
try:
    with open("main.py") as file:
        print("File opened.")
    age = int(input("Age: "))
    xfactor = 10 / age
except (ValueError, ZeroDivisionError):
    print("You didn't input a valid age.")
else:
   print("No exceptions were thrown.")
```

### Exceptions 6 - Raising Exceptions

*Google `python 3 built-in exceptions`*

```python
def calculate_xfactor(age):
    if age <= 0:
        raise ValueError("Age cannot be 0 or less.")
    return 10 / age

try:
    calculate_xfactor(-1)
except ValueError as error:
    print(error)
```
```output
Age cannot be 0 or less.
```

### Exceptions 7 - Cost of Raising Exceptions

```python
from timeit import timeit

code1 = """
def calculate_xfactor(age):
    if age <= 0:
        raise ValueError("Age cannot be 0 or less.")
    return 10 / age

try:
    calculate_xfactor(-1)
except ValueError as error:
    pass
"""

code2 = """
def calculate_xfactor(age):
    if age <= 0:
        return None
    return 10 / age

xfactor = calculate_xfactor(-1)
if xfactor == None:
    pass
"""

print("first code = ", timeit(code1, number=10000))
print("second code = ", timeit(code2, number=10000))
```
```output
first code =  0.004801836
second code =  0.0018724469999999993
```
***Use exception if it has to!***


## Classes 
### Classes - 1 - Introduction

### Classes - 2 - Creating Classes

```python
class Point:
    def draw(self):
        print("draw")

point = Point()
print(type(point))
print(isinstance(point, Point))
```
```output
<class '__main__.Point'>
True
```

### Classes - 3 - Constructors

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y


    def draw(self):
        print(f"Point {self.x}, {self.y}")

point = Point(6, 7)
point.draw()
```

### Classes - 4 - Class vs Instance Attributes

```python
class Point:
    default_color = "red"

    def __init__(self, x, y):
        self.x = x
        self.y = y

    def draw(self):
        print(f"Point {self.x}, {self.y}")

point = Point(6, 7)
point.draw()
print(point.default_color)
point.default_color = "yellow"
print(point.default_color)
```
```output
Point 6, 7
red
yellow
```

### Classes - 5 - Class vs Instance Methods

```python
class Point:

    def __init__(self, x, y):
        self.x = x
        self.y = y

    @classmethod
    def zero(cls):
        return cls(0, 0)

    def draw(self):
        print(f"Point {self.x}, {self.y}")

point = Point.zero()
point.draw()
```
```output
Point 0, 0
```

### Classes - 6 - Magic Methods

*Google `python 3 magic methods`.*

```python
class Point:

    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        return f"({self.x}, {self.y})"

    def draw(self):
        print(f"Point {self.x}, {self.y}")

point = Point(6, 7)
print(point)
```

### Classes - 7 - Comparing Objects

```python
class Point:

    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __eq__(self, other):
        return (self.x == other.x and self.y == other.y)

    def __gt__(self, other):
        return (self.x > other.x and self.y > other.y)

    def draw(self):
        print(f"Point {self.x}, {self.y}")


point = Point(6, 7)
other = Point(6, 7)
print(point == other)
zero = Point(0, 0)
print(point > zero)
```
```output
True
True
```

### Classes - 8 - Performing Arithmetic Operations

```python
class Point:

    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __str__(self):
        return f"({self.x}, {self.y})"

    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)

point = Point(6, 7)
other = Point(6, 7)
print(point + other)
```
```output
(12, 14)
```

### Classes - 9 -  Making Custom Containers

```python
class TagCloud:
    def __init__(self):
        self.tags = {}

    def add(self, tag):
        self.tags[tag.lower()] = self.tags.get(tag.lower(), 0) + 1

    def __getitem__(self, item):
        return self.tags.get(item)

    def __setitem__(self, key, value):
        self.tags[key.lower()] = value

    def __len__(self):
        return len(self.tags)

    def __iter__(self):
        return iter(self.tags)


cloud = TagCloud()
cloud.add("python")
cloud.add("Python")
cloud.add("python")
cloud.add("python")
print(cloud.tags)
print(cloud["python"])
cloud["python"] = 10
print(cloud["python"])
print(len(cloud))
cloud.add("cpp")
cloud.add("c")
print(cloud.tags)
print(len(cloud))
for k in cloud:
    print(f"{k}: {cloud[k]}")
```
```output
{'python': 4}
4
10
1
{'python': 10, 'cpp': 1, 'c': 1}
3
python: 10
cpp: 1
c: 1
```


### Classes - 10 -  Private Members

```python
class TagCloud:
    def __init__(self):
        self.__tags = {}

    def add(self, tag):
        self.__tags[tag.lower()] = self.__tags.get(tag.lower(), 0) + 1

    def __getitem__(self, item):
        return self.__tags.get(item)

    def __setitem__(self, key, value):
        self.__tags[key.lower()] = value

    def __len__(self):
        return len(self.__tags)

    def __iter__(self):
        return iter(self.__tags)


cloud = TagCloud()
print(cloud.__dict__)  # {'_TagCloud__tags': {}}
cloud.add("python")
cloud.add("cpp")

"""
Tricks to access "private" members
"""
print(cloud.__dict__)
print(cloud._TagCloud__tags)
cloud._TagCloud__tags["python"] = 3
print(cloud.__dict__)
```

### Classes - 11 -  Properties

```python
class Product:
    def __init__(self, price):
        self.price = price

    @property
    def price(self):
        return self.__price

    @price.setter
    def price(self, value):
        if value < 0:
            raise ValueError("Price can not be negative.")
        self.__price = value


product = Product(70)
print(product.price)
product.price = 7
print(product.price)
```
```output
70
7
```

### Classes - 12 -  Inheritance


```python
class Animal:
    def __init__(self):
        self.age = 1

    def move(self):
        print("move")

    def eat(self):
        print("eat")


class Fish(Animal):
    def swim(self):
        print("swim")

fish = Fish()
print(fish.age)
fish.move()
fish.eat()
fish.swim()
```
```output
1
move
eat
swim
```

### Classes - 13 -  The Object Class

```python
class Animal:
    def move(self):
        pass
#   Animal: Parent, Base
#   Momall: Child, Sub

class Mammal(Animal):
    def move(self):
        pass

m = Mammal()
print(isinstance(m, Animal))
print((issubclass(Mammal, Animal)))
print(isinstance(m, object))
print((issubclass(Mammal, object)))
```
```output
True
True
True
True
```

### Classes - 14 -  Method Overriding

```python
class Animal:
    def __init__(self):
        print("Animal Constructor")
        self.age = 1

    def move(self):
        print("move")

    def eat(self):
        print("eat")


class Fish(Animal):
    def __init__(self):
        super().__init__()
        print("FIsh Constructor")

    def swim(self):
        print("swim")

    def move(self):
        self.swim()

fish = Fish()
print(fish.age)
fish.move()
fish.eat()
fish.swim()
```
```output
Animal Constructor
FIsh Constructor
1
swim
eat
swim
```

### Classes - 15 - Multi-level Inheritance

***Should avoid it all the time!***


### Classes - 16 - Multiple Inheritance

```python
class Employee:
    def greet(self):
        print("Employee Greet")

class Player:
    def greet(self):
        print("Player Greet")

class Manager(Employee, Player):
    pass

manager = Manager()
manager.greet()
```
```output
Employee Greet
```

### Classes - 17 - A Good Example of Inheritance

```python
class InvalidOperationError(Exception):
    pass

class Stream:
    def __init__(self):
        self.opened = False

    def open(self):
        if self.opened:
            raise InvalidOperationError("Stream is already opened")
        self.opened = True

    def close(self):
        if not self.opened:
            raise InvalidOperationError("Stream is already closed")
        self.opened = False


class FileStream(Stream):
    def read(self):
        print("Reading data from a file")


class NetworkStream(Stream):
    def read(self):
        print("Reading data from a network")
```

### Classes - 18 - Abstract Base Classes

```python
from abc import ABC, abstractmethod

class InvalidOperationError(Exception):
    pass

class Stream(ABC):
    def __init__(self):
        self.opened = False

    def open(self):
        if self.opened:
            raise InvalidOperationError("Stream is already opened")
        self.opened = True

    def close(self):
        if not self.opened:
            raise InvalidOperationError("Stream is already closed")
        self.opened = False

    @abstractmethod
    def read(self):
        pass


class FileStream(Stream):
    def read(self):
        print("Reading data from a file")


class NetworkStream(Stream):
    def read(self):
        print("Reading data from a network")
        
```

### Classes - 19 - Polymorphism

```python
from abc import ABC, abstractmethod

class UIControl(ABC):

    @abstractmethod
    def draw(self):
        pass

class TextBox(UIControl):
    def draw(self):
        print("TextBox")

class DropDownList(UIControl):
    def draw(self):
        print("DropDownList")

def draw(controls):
    for control in controls:
        control.draw()

ddl = DropDownList()
tb = TextBox()
draw([ddl, tb])
```

### Classes - 20 - Duck Typing

```python
class TextBox():
    def draw(self):
        print("TextBox")

class DropDownList():
    def draw(self):
        print("DropDownList")

def draw(controls):
    for control in controls:
        control.draw()

ddl = DropDownList()
tb = TextBox()
draw([ddl, tb])
```

### Classes - 21 - Extending Built-in Types

```python
class Text(str):
    def duplicate(self):
        return self + self

class TrackableList(list):
    def append(self, object):
        print("Append called")
        super().append(object)

text = Text("Python")
print(text.duplicate())
print(text.lower())

list = TrackableList()
list.append("1")
print(list)
```
```output
PythonPython
python
Append called
['1']
```

### Classes - 22 - Data Classes

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __eq__(self, other):
        return self.x == other.x and self.y == other.y

p1 = Point(1, 2)
p2 = Point(1, 2)
print(hex(id(p1)))
print(hex(id(p2)))
print(p1 == p2)
```
```output
0x7fe9ac798dc0
0x7fe9ada000a0
True
```

```python
from collections import namedtuple

Point = namedtuple("Point", ["x", "y"])

p1 = Point(x=1, y=2)
p2 = Point(1, 2)
print(hex(id(p1)))
print(hex(id(p2)))
print(p1 == p2)

# p1.x = 10 # Error! nametuple is immutable
p1 = Point(x=10, y=2)
print(p1)
```
```output
0x7fcf1fa17280
0x7fcf1fa54b00
True
Point(x=10, y=2)
```


## Python Standard Library

### Python Standard Library - 1 - Introduction

### Python Standard Library - 2 - Working With Paths

```python
from pathlib import Path

Path(r"C:\Program Files\Microsoft")
Path("/usr/local/bin")
Path()
Path("ecommerce/__init__.py")
Path() / "ecommerce" / "__init__.py"
Path.home()
```

*Google `python 3 pathlib`*

```python
from pathlib import Path

path = Path("ecommerce/__init__.py")
print(path.exists())
print(path.is_dir())
print(path.is_file())
print(path.name)
print(path.stem)
print(path.suffix)
print(path.parent)
new_path = path.with_name("file.txt")
print(path.absolute())
print(new_path.absolute())
suf_path = path.with_suffix(".txt")
print(suf_path)
```
```output
True
False
True
__init__.py
__init__
.py
ecommerce
/Users/mac/PycharmProjects/demo/ecommerce/__init__.py
/Users/mac/PycharmProjects/demo/ecommerce/file.txt
ecommerce/__init__.txt
```

### Python Standard Library - 3 - Working With Directories

```python
from pathlib import Path

path = Path("ecommerce")

paths = [p for p in path.iterdir() if p.is_dir()]
py_files = [p for p in path.glob("*.py")]
recursive_py_files = [p for p in path.rglob("*.py")]
print(paths)
print(py_files)
print(recursive_py_files)
```
```output
[PosixPath('ecommerce/shopping'), PosixPath('ecommerce/customer')]
[PosixPath('ecommerce/__init__.py')]
[PosixPath('ecommerce/__init__.py'), PosixPath('ecommerce/shopping/__init__.py'), PosixPath('ecommerce/customer/__init__.py')]
```

### Python Standard Library - 4 - Working With Files

```python
from pathlib import Path
from time import ctime

path = Path("ecommerce/__init__.py")
# path.exists()
# path.rename("init.txt")
# path.unlink()
print(path.stat())
print(ctime(path.stat().st_ctime))
```
```output
os.stat_result(st_mode=33188, st_ino=12893556958, st_dev=16777220, st_nlink=1, st_uid=501, st_gid=20, st_size=0, st_atime=1641648319, st_mtime=1641648319, st_ctime=1641648319)
Sat Jan  8 21:25:19 2022
```

```python
path.read_text()
path.read_bytes()
path.write_text("...")
path.write_bytes(b'000111')
```

```python
from pathlib import Path
import shutil

source = Path("ecommerce/__init__.py")
target = Path() / "__init__.py"

# target.write_text((source.read_text()))
shutil.copy(source, target)
```

### Python Standard Library - 5 - Working Zip Paths

```python
from pathlib import Path
from zipfile import ZipFile

# with ZipFile("files.zip", "w") as z:
#     for path in Path("ecommerce").rglob("*.*"):
#         z.write(path)

with ZipFile("files.zip") as zip:
    print(zip.namelist())
    info = zip.getinfo("ecommerce/__init__.py")
    print(info.file_size)
    print(info.compress_size)

    # Extract all the files to the folder named "extract"
    zip.extract("extract")
```
```output
['ecommerce/__init__.py', 'ecommerce/shopping/__init__.py', 'ecommerce/customer/__init__.py']
0
0
```

### Python Standard Library - 6 - Working With CSV Files

```python
import csv

with open("data.csv", "w") as file:
    writer = csv.writer(file)
    writer.writerow(["transaction_id", "product_id", "price"])
    writer.writerow([1000, 1, 5])
    writer.writerow([1001, 2, 15])

with open("data.csv") as file:
    reader = csv.reader(file)
    # print(list(reader)) # Only iterate once
    for row in reader:
        print(row)

```
```output
['transaction_id', 'product_id', 'price']
['1000', '1', '5']
['1001', '2', '15']
```

### Python Standard Library - 7 - Working With JSON Paths

```python
import json
from pathlib import Path

movies = [
    {"id": 1, "title": "Terminator", "year": 1990},
    {"id": 2, "title": "Kindergarten Cop", "year": 1993}
]

data = json.dumps(movies)
Path("movies.json").write_text(data)

json_data = Path("movies.json").read_text()
print(json_data)
```
```output
[
    {"id": 1, "title": "Terminator", "year": 1990},
    {"id": 2, "title": "Kindergarten Cop", "year": 1993}
]
```

### Python Standard Library - 8 - Working a SQLite Database

- *Download and instlall `sqlite db browser`.*
- *Create a new database and table before running python program.*

```python
import sqlite3
import json
from pathlib import Path

movies = json.loads(Path("movies.json").read_text())
print(movies)

with sqlite3.connect("db.sqlite3") as conn:
    command = "INSERT INTO movies VALUES(?, ?, ?)"
    for movie in movies:
        conn.execute(command, tuple(movie.values()))
    conn.commit()
```
=> *To browsing the db browser.*

```python
import sqlite3

with sqlite3.connect("db.sqlite3") as conn:
    command = "SELECT * FROM Movies"
    cursor = conn.execute(command)
    # for row in cursor: # cursor only can be iterated once
    #     print(row)

    movies = cursor.fetchall()
    print(movies)
```
```output
[(1, 'Terminator', 1990), (2, 'Kindergarten Cop', 1993)]
```

### Python Standard Library - 9 - Working With Timestamps

```python
import time

def send_emails():
    for i in range(1000000):
        pass

start = time.time()
send_emails()
end = time.time()
duration = end - start
print(duration)
```
```output
0.03973817825317383
```

### Python Standard Library - 10 - Working With DateTimes

```python
from datetime import datetime
import time

print(datetime(2022, 1, 10))
print(datetime.now())
print(datetime.strptime("2021/01/10", "%Y/%m/%d"))
dt = datetime.fromtimestamp(time.time())
print(dt)
print(f"{dt.year}/{dt.month}")
print(dt.strftime("%Y/%m"))
```
```output
2022-01-10 00:00:00
2022-01-10 22:14:43.650436
2021-01-10 00:00:00
2022-01-10 22:14:43.673962
2022/1
2022/01
```

### Python Standard Library - 11 - Working with Time Deltas

```python
from datetime import datetime, timedelta

dt1 = datetime(2020, 1, 1) + timedelta(days=1, seconds=1000)
dt2 = datetime.now()

duration = dt2 - dt1
print(duration)
print('days', duration.days)
print('seconds', duration.seconds)
print('total_seconds', duration.total_seconds())
```
```output
747 days, 22:03:57.331225
days 747
seconds 79437
total_seconds 64620237.331225
```

### Python Standard Library - 12 - Generating Random Values

```python
import random
import string

print(random.random())
print(random.randint(1, 10))
print(random.choice([1, 2, 3, 4, 5, 6, 7]))
print(random.choices([1, 2, 3, 4, 5, 6, 7], k=2))
print(random.choices([1, 2, 3, 4, 5, 6, 7], k=4))
print(random.choices('hello lawjune', k=4))
print("".join(random.choices('hello lawjune', k=4)))
print(",".join(random.choices('hello lawjune', k=4)))

print(string.ascii_letters)
print(string.digits)

print("Random Password:", "".join(random.choices(string.ascii_letters + string.digits, k=6)))
```
```output
0.7916912303647569
6
6
[4, 7]
[3, 5, 6, 5]
['j', 'w', 'n', 'u']
 lau
a,u,n,u
abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
0123456789
Random Password: cpzDjP
```

### Python Standard Library - 13 - Opening the Browser

```python
import webbrowser

print("Deployment completed")
webbrowser.open("http://google.com")
```

### Python Standard Library - 14 - Sending Emails

```python
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.image import MIMEImage
from pathlib import Path
import smtplib

message = MIMEMultipart()
message["from"] = "18516315041@163.com"
message["to"] = "lawjune@163.com"
message["subject"] = "This is a test"
message.attach(MIMEText("Body"))
message.attach(MIMEImage(Path("me.jpg").read_bytes()))

with smtplib.SMTP_SSL(host="smtp.163.com", port=465) as smtp:
    smtp.ehlo()
    # smtp.starttls()
    smtp.login("18516315041@163.com", "cheryl1108")
    smtp.send_message(message)
    print("Sent...")
```

### Python Standard Library - 15 - Templates

```python
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.image import MIMEImage
from pathlib import Path
from string import Template
import smtplib

template = Template(Path("template.html").read_text())

message = MIMEMultipart()
message["from"] = "18516315041@163.com"
message["to"] = "lawjune@163.com"
message["subject"] = "This is a test"
body = template.substitute({"name": "Jun"})
message.attach(MIMEText(body, "html"))
message.attach(MIMEImage(Path("me.jpg").read_bytes()))

with smtplib.SMTP_SSL(host="smtp.163.com", port=465) as smtp:
    smtp.ehlo()
    # smtp.starttls()
    smtp.login("18516315041@163.com", "cheryl1108")
    smtp.send_message(message)
    print("Sent...")
```

```html
<!doctype html>
<html lang="en">
<head>
</head>
<body>
    Hi <strong>$name</strong>, this is our test email.
</body>
</html>
```

### Python Standard Library - 16 - Command-line Arguments

```python
import sys

if len(sys.argv) == 1:
    print("USAGE: python main.py <password>")
else:
    password = sys.argv[1]
    print("Password", password)
```
```sh
python main.py -a -b -c
`=>
Password -a
```

### Python Standard Library - 17 - Running External Programs

```python
import subprocess

"""
Old legacy:
subprocess.call()
subprocess.check_call()
subprocess.check_output()
subprocess.Popen
"""

completed = subprocess.run(["ls", "-lart"],
                           capture_output=True,
                           text=True)
print("args", completed.args)
print("returncode", completed.returncode)
print("stderr", completed.stderr)
print("stdout", completed.stdout)
```
```output
args ['ls', '-lart']
returncode 0
stderr 
stdout total 160
-rw-r--r--@  1 mac  staff  40289 Aug  3 23:29 me.jpg
-rw-r--r--   1 mac  staff    412 Jan  8 22:00 files.zip
drwxr-xr-x   8 mac  staff    256 Jan 10 21:33 .idea
drwxr-xr-x   6 mac  staff    192 Jan 10 21:35 ecommerce
drwxr-xr-x   7 mac  staff    224 Jan 10 21:35 venv
drwxr-xr-x   6 mac  staff    192 Jan 10 21:35 ..
-rw-r--r--@  1 mac  staff     54 Jan 10 21:38 data.csv
-rw-r--r--   1 mac  staff    102 Jan 10 21:45 movies.json
-rw-r--r--   1 mac  staff  12288 Jan 10 21:58 db.sqlite3
-rw-r--r--@  1 mac  staff   6148 Jan 18 22:50 .DS_Store
-rw-r--r--   1 mac  staff    125 Jan 18 23:04 template.html
-rw-r--r--   1 mac  staff    395 Jan 18 23:20 main.py
drwxr-xr-x  13 mac  staff    416 Jan 18 23:20 .
```

```python
import subprocess

completed = subprocess.run(["python", "other.py"],
                           capture_output=True,
                           text=True)
print("args", completed.args)
print("returncode", completed.returncode)
print("stderr", completed.stderr)
print("stdout", completed.stdout)
```
```output
args ['python', 'other.py']
returncode 0
stderr 
stdout This is a complicated program!
```

```python
import subprocess

try:
    completed = subprocess.run(["false"],
                               capture_output=True,
                               text=True,
                               check=True)
except subprocess.CalledProcessError as ex:
    print(ex)
```
```output
Command '['false']' returned non-zero exit status 1.
```

## Python Package Index

### Python Package Index - 1 - Pypi

```sh
pip3 list
`=>
Package                           Version
--------------------------------- ---------
backports.entry-points-selectable 1.1.0
certifi                           2021.10.8
distlib                           0.3.3
filelock                          3.3.2
pip                               21.2.3
pipenv                            2021.5.29
platformdirs                      2.4.0
setuptools                        57.4.0
six                               1.16.0
virtualenv                        20.10.0
virtualenv-clone                  0.5.7
WARNING: You are using pip version 21.2.3; however, version 21.3.1 is available.
You should consider upgrading via the '/Library/Frameworks/Python.framework/Versions/3.10/bin/python3.10 -m pip install --upgrade pip' command.
```

```sh
pip3 install --upgrade pip
```

```sh
pip3 install requests
pip3 list
`=>
Package                           Version
--------------------------------- ---------
backports.entry-points-selectable 1.1.0
certifi                           2021.10.8
charset-normalizer                2.0.10
distlib                           0.3.3
filelock                          3.3.2
idna                              3.3
pip                               21.3.1
pipenv                            2021.5.29
platformdirs                      2.4.0
requests                          2.27.1
setuptools                        57.4.0
six                               1.16.0
urllib3                           1.26.8
virtualenv                        20.10.0
virtualenv-clone                  0.5.7
```

```sh
pip3 install requests==2.20.*
```

```sh
pip3 install requests~=2.20.0
```

```sh
pip3 uninstall requests
```

### Python Package Index - 3 - Virtual Environments

```sh
python3 -m venv env
source env/bin/activate
```

```sh
deactivate
```

### Python Package Index - 4 - Pipenv

*Combind pip and virtualenv.*

```sh
pip3 install pipenv
```

```sh
pipenv install requests
```

```sh
pipenv --venv
`=>
/Users/mac/.local/share/virtualenvs/pythondemo-kvyUC8O7
```

***Activate***
```sh
pipenv shell
```

```sh
exit
```

### Python Package Index - 5 - Virtual Environments in VSCode

### Python Package Index - 6 - Pipfile

```sh
➜  pythondemo pipenv --venv
`=>
/Users/mac/.local/share/virtualenvs/pythondemo-kvyUC8O7
➜  pythondemo rm -rf /Users/mac/.local/share/virtualenvs/pythondemo-kvyUC8O7
➜  pythondemo pipenv --venv
`=>
No virtualenv has been created for this project(/Users/mac/Projects/pythondemo) yet!
Aborted!
```

```sh
pipenv install
pipenv --venv
`=>
/Users/mac/.local/share/virtualenvs/pythondemo-kvyUC8O7
```

**Use the pipfile.lock**
```sh
pipenv install --ignore-pipfile
```

### Python Package Index - 7 - Managing Dependencies

```sh
pipenv graph
requests==2.27.1
  - certifi [required: >=2017.4.17, installed: 2021.10.8]
  - charset-normalizer [required: ~=2.0.0, installed: 2.0.10]
  - idna [required: >=2.5,<4, installed: 3.3]
  - urllib3 [required: >=1.21.1,<1.27, installed: 1.26.8]
```

**The dependencies leave after removing the `requests` package**
*But the left dependencies will not be installed in another new machine.*
```sh
pipenv uninstall requests
pipenv graph
`=>
certifi==2021.10.8
charset-normalizer==2.0.10
idna==3.3
urllib3==1.26.8
```

```sh
pipenv update --outdated
```
*To modify the as the latest version if receiving warning.*

### Python Package Index - 8 - Publishing Packages

```sh
 pip3 install setuptools wheel twine
 ```

 https://choosealicense.com/

*sdist - short distribution*
*bdist_wheel - build distribution*
```sh
python3 setup.py sdist bdist_wheel
```

*setup.py*
```python
import setuptools
from pathlib import Path

setuptools.setup(
    name="ljpdf",
    version=1.0,
    long_desription=Path("README.md").read_text(),
    packages=setuptools.find_packages(exclude=["tests", "data"])
)
```

```sh
twine upload dist/*
```

### Python Package Index - 9 - Docstrings

""" One line description.

    A more detailed explanation.
"""

```python
""" This module provides functions to convert a PDF to text. """

def convert():
    """ 
    Convert the given PDF to text. 

    Parameters:
    path (str): The path to a PDF file.

    Returns:
    str: The content of the PDF file a text.    
    """
    print("pdf2text")
```

```python
""" This module provides functions to convert a PDF to image. """

class ImageConverter:
    """ A simple converter for converting PDFs to image."""

    def convert(path):
        """ 
        Convert the given PDF to image. 

        Parameters:
        path (str): The path to a PDF file.

        Returns:
        str: The content of the PDF file a image.    
        """
        print("pdf2text")
```

### Python Package Index - 10 - Pydoc

```sh
pydoc3 math
```

```sh
pydoc3 -w ljpdf.pdf2image
`=>
wrote ljpdf.pdf2image.html
```
```sh
ls | grep html
`=>
jpdf.pdf2image.html
```

```sh
ljpdf pydoc3 -p 1234
`=>
pydoc server ready at http://localhost:1234/
```

## Populate Python Packages

### Populate Python Packages - 1 - Introduction

- Excel Spreadsheet
- PDFs
- Sending Text
- Browser Automation
- Web Scraping

### Populate Python Packages - 2 - What are APIs

### Populate Python Packages - 3 - Yelp API

https://www.yelp.com/developers

*To create an app*

Client ID
awDq-mwWxAWrJY7dncThUg

API Key
KtpK3R419eapFObedVBP_9b1vfz4u-JFdTIuWf8qQRF19107F-JymsgkwHeM6tEV69aGwmbrMpJLj3XFkzYrF8rj8Z4Cxxn90dzKQWGeqoE_ZF9SACTDns0kb3rpYXYx

### Populate Python Packages - 4 - Searching for Businesses

```python
import requests

url = "https://api.yelp.com/v3/businesses/search"
api_key = "KtpK3R419eapFObedVBP_9b1vfz4u-JFdTIuWf8qQRF19107F-JymsgkwHeM6tEV69aGwmbrMpJLj3XFkzYrF8rj8Z4Cxxn90dzKQWGeqoE_ZF9SACTDns0kb3rpYXYx"
headers = {
    "Authorization": "Bearer " + api_key
}

params = {
    "term": "Barber",
    "location": "NYC"
}

response = requests.get(url, headers=headers, params=params)
businesses = response.json()['businesses']
names = [business['name'] for business in businesses if business['rating'] > 4.5] 
print(names)
```
```output
['Next Level Barber Shop', 'The Kinsman Barber Shop', '12 Pell', "Barber's Point", 'Hairrari East Village', 'The Flying Row']
```

### Populate Python Packages - 5 - Hiding API Keys

### Populate Python Packages - 6 - Sending Text Messages

https://console.twilio.com/?frameUrl=%2Fconsole%3Fx-target-region%3Dus1&newCustomer=true
Jluo33@shcheryl1108

### Populate Python Packages - 7 - Web Scraping

```python
import requests
from bs4 import BeautifulSoup

response =requests.get("https://stackoverflow.com/questions")
soup = BeautifulSoup(response.text, "html.parser")

questions = soup.select(".question-summary")
# print(type(questions))
# print(questions[0].attrs)
# print(questions[0].get("id", 0))
# print(questions[0].select(".question-hyperlink"))
# print(questions[0].select_one(".question-hyperlink").get_text())
for question in questions:
    print(question.select_one(".question-hyperlink").get_text())
    print(question.select_one(".vote-count-post").get_text)
```

### Populate Python Packages - 8 - Browser Automation

*Install the driver*
*Search `selenium` in https://pypi.org/*

```sh
cp chromedriver /usr/local/bin
```

```python
from selenium import webdriver

browser = webdriver.Chrome()
browser.get("https://github.com")

signin_Link = browser.find_element_by_link_text("Sign in")
signin_Link.click()

username_box = browser.find_element_by_id("login_field")
username_box.send_keys("Lawjune")
password_box = browser.find_element_by_id("password")
password_box.send_keys("Jluo33@sh")
password_box.submit()

assert "Lawjune" in browser.page_source

profile_link = browser.find_element_by_class_name("user-profile-link")
link_label = profile_link.get_attribute("innerHTML")
assert "Lawjune" in link_label

browser.quit()
```

https://selenium-python.readthedocs.io/
***TO READ `Waits` and `Page Object` to organize re-used objects***
5. Waits
5.1. Explicit Waits
5.2. Implicit Waits
6. Page Objects
6.1. Test case
6.2. Page object classes
6.3. Page elements
6.4. Locators

### Populate Python Packages - 9 - Working with PDFs

```sh
pipenv install pypdf2
```

```python
import PyPDF2

with open("first.pdf", "rb") as file:
    reader = PyPDF2.PdfFileReader(file)
    print(reader.numPages)
    page = reader.getPage(0)
    page.rotateClockwise(90)
    writer = PyPDF2.PdfFileWriter()
    writer.addPage(page)
    with open("rotated.pdf", "wb") as output:
        writer.write(output)
```

```python
import PyPDF2

merger = PyPDF2.PdfFileMerger()
file_names = ["first.pdf", "second.pdf"]
for file_name in file_names:
    merger.append(file_name)
merger.write("combined.pdf")
```

### Populate Python Packages - 10 - Working with Excel Spreadsheets

```python
import openpyxl

# wb = openpyxl.Workbook()
wb = openpyxl.load_workbook("transactions.xlsx")
print(wb.sheetnames)

sheet = wb["Sheet1"]
# wb.create_sheet("Sheet2", 0)

cell = sheet["a1"] # cell = sheet.cell(row=1, column=1)
# print(cell.value)
# print(cell.row)
# print(cell.column)
# print(cell.coordinate)

for row in range(1, sheet.max_row + 1):
    for column in range(1, sheet.max_column + 1):
        cell = sheet.cell(row, column)
        print(cell.value)

column = sheet["a"]
print(column)

cells = sheet["a:c"]
print(cells)

print(sheet["a1:c3"])

sheet.append([1, 2, 3])
# sheet.insert_rows

wb.save("transactions2.xlsx")
```

### Populate Python Packages - 11 - Command Query Separation Principle

```python
import openpyxl

wb = openpyxl.load_workbook("transactions.xlsx")

sheet = wb["Sheet1"]
for row in range(1, 10):
    cell = sheet.cell(row, 1) # Violated the query separation principle here, which will unexpectedly create new rows
    print(cell.value)

sheet.append([1, 2, 3]) # Actually appended after 5 empty rows
wb.save("transactions2.xlsx")
```

### Populate Python Packages - 12 - NumPy

```python
import numpy as np

array = np.array([ [1, 2, 3], [4, 5, 6] ])
print(type(array))
print(array)
print(array.shape)
```
```output
<class 'numpy.ndarray'>
[[1 2 3]
 [4 5 6]]
(2, 3)
```

```python
import numpy as np

# array = np.zeros((4, 7), dtype=int)
# print(array)

# array = np.ones((4, 7), dtype=int)
# print(array)

# array = np.full((4, 7), 7, dtype=int)
# print(array)

array = np.random.random((4, 7))
# print(array)
# print(array[0, 0])
print(array > 0.4)
print(array[array > 0.4])
print(np.sum(array))
print(np.round(array))
```
```output
[[False False  True  True  True False  True]
 [False  True  True  True False  True False]
 [ True  True  True False  True False  True]
 [ True False False False  True  True False]]
[0.77559397 0.64522334 0.98530438 0.98014357 0.68748266 0.77433526
 0.78416883 0.60188274 0.70635682 0.4800991  0.76557062 0.93770749
 0.60251335 0.74376297 0.79870406 0.88573593]
14.607254974067338
[[0. 0. 1. 1. 1. 0. 1.]
 [0. 1. 1. 1. 0. 1. 0.]
 [1. 0. 1. 0. 1. 0. 1.]
 [1. 0. 0. 0. 1. 1. 0.]]
```

```python
import numpy as np

first = np.array([1, 2, 3])
second = np.array([1, 2, 3])
print(first + second)
print(first + 4)
```
```output
[2 4 6]
[5 6 7]
```

```python
import numpy as np

dimensions_inch = np.array([1, 2, 3])
dimensions_cm = dimensions_inch * 2.54

print(dimensions_cm)

dimensions_inch = [1, 2, 3]
dimensions_cm = [x * 2.54 for x in dimensions_inch]
print(dimensions_cm)
```
```output
[2.54 5.08 7.62]
[2.54, 5.08, 7.62]
```

## Machine Learning with Python


### Machine Learning with Python - 1 - What is Machine Learning

### Machine Learning with Python - 2 - Machine Learning in Action

**Steps**
1. Import the Data
2. Clean the Data
3. Split the Data into Training/Test Sets
4. Create a Model
5. Train the Model
6. Make Predictions
7. Evaluate and Improve

### Machine Learning with Python - 3 - Libraries and Tools
- **Numpy**
- **Pandas**
- **MatPlotLib**
- **Scikit-Learn**


### Machine Learning with Python - 4 - mporting a Data Set

https://www.kaggle.com/
https://www.kaggle.com/gregorut/video-game-sales-study
        
### Machine Learning with Python - 5 - Jupyter Shortcuts

### Machine Learning with Python - 6 - A Real Machine Learning Problem

### Machine Learning with Python - 7 - Preparing the Data

### Machine Learning with Python - 8 - Learning and Predicting

```python
import pandas as pd
from sklearn.tree import DecisionTreeClassifier
music_data = pd.read_csv('music.csv')
x = music_data.drop(columns=['genre'])
y = music_data['genre']

model = DecisionTreeClassifier()
model.fit(x, y)
predictions = model.predict([ [21, 1], [22, 0] ])
predictions
```
```output
array(['HipHop', 'Dance'], dtype=object)
```

### Machine Learning with Python - 9 - Calculating Accuracy

```python
import pandas as pd
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

music_data = pd.read_csv('music.csv')
x = music_data.drop(columns=['genre'])
y = music_data['genre']
x_train, x_test, y_train, y_test = train_test_split(x, y, test_size=0.2)

model = DecisionTreeClassifier()
model.fit(x_train, y_train)
predictions = model.predict(x_test)

score = accuracy_score(y_test, predictions)
score
```

`ctrl` + `enter` in jupyter notebook


### Machine Learning with Python - 10 - Persisting Models

*Dump*
```python
import pandas as pd
from sklearn.tree import DecisionTreeClassifier
import joblib

music_data = pd.read_csv('music.csv')
x = music_data.drop(columns=['genre'])
y = music_data['genre']

model = DecisionTreeClassifier()
model.fit(x, y)

joblib.dump(model, 'music-recommender.joblib')

# predictions = model.predict([ [21, 1], [22, 0] ])
# predictions
```

*Load*
```python
model = joblib.load('music-recommender.joblib')
predictions = model.predict([ [21, 1], [22, 0] ])
predictions
```

### Machine Learning with Python - 11 - Visualizing a Decision Tree



















































