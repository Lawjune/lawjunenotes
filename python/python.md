## Data Structures
### 1 - Lists
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

### 2 - Accessing Items
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

### 3 - List Unpacking

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

### 4 - Looping over Lists

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

### 5 - Adding or Removing Items

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

### 6 - Finding Items

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

### 7 - Sorting Lists

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

### 8 - Lambda Functions

```python
items = [
    ("product1", 10),
    ("product2", 9),
    ("product3", 12),
]

items.sort(key=lambda item:item[1])
print(items)
```

### 9 - Map Function

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




































