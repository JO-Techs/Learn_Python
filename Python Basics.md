# Python Basics Cheat Sheet 

A concise guide to essential Python functions and concepts.

## 1. Print & Input
```python
print("Hello, World!")  # Output text
name = input("Enter your name: ")  # Read user input
```

## 2. Variables & Comments
```python
x = 10  # Assign a value
# This is a comment
"""This is a multi-line docstring."""
```

## 3. Conditional Statements
```python
if x > 5:
    print("x is large")
elif x == 5:
    print("x is 5")
else:
    print("x is small")
```

## 4. Loops
```python
for i in range(5):
    print(i)  # 0 to 4

while x < 5:
    x += 1
```

## 5. Loop Control
```python
if x == 3:
    break  # Exit loop
if x == 3:
    continue  # Skip iteration

def empty():
    pass  # Placeholder
```

## 6. Functions
```python
def greet():
    print("Hello!")

def add(a, b):
    return a + b

square = lambda x: x ** 2  # Anonymous function
```

## 7. Data Types & Conversion
```python
num = int("10")
text = str(10)
pi = float("3.14")
flag = bool(1)
```

## 8. Data Structures
```python
numbers = list(range(3))  # [0, 1, 2]
coordinates = tuple([1, 2])  # (1, 2)
person = {"name": "Alice", "age": 30}  # Dictionary
unique = {1, 1, 2}  # Set: {1, 2}
```

## 9. Common Functions
```python
len("Hello")  # Length of object
range(5)  # Generates sequence 0-4
```

## 10. List Methods
```python
nums.append(3)  # Add item
nums.remove(2)  # Remove first match
nums.pop(0)  # Remove by index
nums.sort(reverse=True)  # Sort list
```

## 11. String Methods
```python
"a,b,c".split(",")  # ['a', 'b', 'c']
"-".join(['a', 'b'])  # "a-b"
"  hi  ".strip()  # "hi"
"Name: {}".format("Alice")
f"Value: {x}"  # f-string
```

## 12. File Handling
```python
with open("data.txt") as file:
    content = file.read()
```

## 13. Modules & Imports
```python
import math
from math import sqrt
```

## 14. Error Handling
```python
try:
    x = 1 / 0
except ZeroDivisionError:
    print("Error!")
finally:
    print("Cleanup")

raise ValueError("Invalid value")
```

## 15. Operators & Keywords
```python
if "a" in ["a", "b"]: ...  # Membership
if x is None: ...  # Identity
if x > 0 and y < 10: ...  # Logical

del my_list[0]  # Delete
print(type(5))  # Get type
```
