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
### Classes - Introduction

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












































