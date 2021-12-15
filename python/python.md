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

















