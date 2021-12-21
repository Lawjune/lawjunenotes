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
























