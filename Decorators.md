# Python Decorators - A Detailed Guide

## Introduction
Decorators are a powerful feature in Python that allow us to modify the behavior of functions or classes **without changing their actual code**. They make code **cleaner, reusable, and more readable**.

This lecture covers:
- Basics of decorators
- Functions as first-class objects
- Creating decorators
- Using `@functools.wraps`
- Decorators with arguments
- Chaining multiple decorators
- Class-based decorators

---

## 1. Functions as First-Class Objects
Python treats functions as **first-class objects**, meaning they can be:
- Assigned to variables
- Passed as arguments
- Returned from functions

```python
# Assigning function to a variable
def greet(name):
    return f"Hello, {name}!"

say_hello = greet
print(say_hello("Alice"))  # Output: Hello, Alice!
```

---

## 2. Understanding Decorators
A **decorator** is a function that **wraps another function** to modify its behavior.

### **Basic Decorator Example**
```python
def my_decorator(func):
    def wrapper():
        print("Something before the function runs.")
        func()
        print("Something after the function runs.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello, World!")

say_hello()
```
**Output:**
```
Something before the function runs.
Hello, World!
Something after the function runs.
```

---

## 3. Using `@functools.wraps`
`functools.wraps` helps preserve the original function name and docstring when using decorators.

```python
from functools import wraps

def my_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print("Executing decorator")
        return func(*args, **kwargs)
    return wrapper

@my_decorator
def add(x, y):
    "Adds two numbers"
    return x + y

print(add.__name__)  # Output: add
print(add.__doc__)   # Output: Adds two numbers
```

---

## 4. Decorators with Arguments
To pass arguments to a decorator, we **nest another function inside it**.

```python
def repeat(n):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for _ in range(n):
                func(*args, **kwargs)
        return wrapper
    return decorator

@repeat(3)
def greet():
    print("Hello!")

greet()
```
**Output:**
```
Hello!
Hello!
Hello!
```

---

## 5. Chaining Multiple Decorators
We can apply **multiple decorators** to a function by stacking them.

```python
def uppercase(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs).upper()
    return wrapper

def exclamation(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs) + "!"
    return wrapper

@uppercase
@exclamation
def greet():
    return "hello"

print(greet())  # Output: HELLO!
```

---

## 6. Class-Based Decorators
We can also use **classes** to create decorators.

```python
class Logger:
    def __init__(self, func):
        self.func = func
    
    def __call__(self, *args, **kwargs):
        print(f"Executing {self.func.__name__}...")
        return self.func(*args, **kwargs)

@Logger
def say_hello():
    print("Hello, World!")

say_hello()
```
**Output:**
```
Executing say_hello...
Hello, World!
```

---

## 7. Practical Use Cases of Decorators
### **Logging Decorator**
```python
import time

def timing(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"{func.__name__} took {end_time - start_time:.5f} seconds")
        return result
    return wrapper

@timing
def slow_function():
    time.sleep(2)
    print("Function finished!")

slow_function()
```
**Output:**
```
Function finished!
slow_function took 2.00034 seconds
```

---

## Conclusion
Decorators are a powerful feature in Python that allow us to modify the behavior of functions in a clean and reusable way. They are widely used in **logging, authentication, timing functions, and access control**.

Would you like to explore **custom decorators** for specific tasks? 🚀
