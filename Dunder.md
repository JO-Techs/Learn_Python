# Understanding Dunder (Double Underscore) Methods in Python

Dunder methods, or magic methods, are special methods in Python that have double underscores
at the beginning and end of their names (e.g., `__init__`, `__str__`). These methods allow classes
to define behavior for built-in operations.

## 1. The `__init__` Method: Constructor Method
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

p = Person("Alice", 30)
print(p.name, p.age)  # Alice 30
```

## 2. The `__str__` and `__repr__` Methods: String Representation
```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def __str__(self):
        return f"Person(name={self.name}, age={self.age})"
    
    def __repr__(self):
        return f"Person('{self.name}', {self.age})"

p = Person("Bob", 25)
print(str(p))   # Calls __str__
print(repr(p))  # Calls __repr__
```

## 3. The `__len__` Method: Length of an Object
```python
class Group:
    def __init__(self, members):
        self.members = members
    
    def __len__(self):
        return len(self.members)

g = Group(["Alice", "Bob", "Charlie"])
print(len(g))  # 3
```

## 4. The `__call__` Method: Making Objects Callable
```python
class Multiplier:
    def __init__(self, factor):
        self.factor = factor
    
    def __call__(self, value):
        return value * self.factor

m = Multiplier(3)
print(m(5))  # 15
```

## 5. The `__getitem__` and `__setitem__` Methods: Indexing Support
```python
class Container:
    def __init__(self):
        self.data = {}
    
    def __getitem__(self, key):
        return self.data.get(key, None)
    
    def __setitem__(self, key, value):
        self.data[key] = value

c = Container()
c["x"] = 10
print(c["x"])  # 10
```

## 6. The `__eq__`, `__lt__`, `__gt__` Methods: Object Comparisons
```python
class Number:
    def __init__(self, value):
        self.value = value
    
    def __eq__(self, other):
        return self.value == other.value
    
    def __lt__(self, other):
        return self.value < other.value
    
    def __gt__(self, other):
        return self.value > other.value

n1 = Number(5)
n2 = Number(10)
print(n1 == n2)  # False
print(n1 < n2)   # True
print(n1 > n2)   # False
```

## 7. The `__add__`, `__sub__`, `__mul__` Methods: Operator Overloading
```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)
    
    def __sub__(self, other):
        return Vector(self.x - other.x, self.y - other.y)

v1 = Vector(2, 3)
v2 = Vector(1, 4)
v3 = v1 + v2  # Calls __add__
v4 = v1 - v2  # Calls __sub__
print(f"v3: ({v3.x}, {v3.y})")  # (3, 7)
print(f"v4: ({v4.x}, {v4.y})")  # (1, -1)
```

## 8. The `__enter__` and `__exit__` Methods: Context Managers
```python
class FileManager:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
    
    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file
    
    def __exit__(self, exc_type, exc_value, traceback):
        self.file.close()

with FileManager("test.txt", "w") as f:
    f.write("Hello, world!")
```

## 9. The `__del__` Method: Destructor
```python
class Temporary:
    def __init__(self, name):
        self.name = name
    
    def __del__(self):
        print(f"Deleting {self.name}")

t = Temporary("TempObj")
del t  # Calls __del__
```

## Conclusion
Dunder methods provide a way to define custom behaviors for built-in operations in Python.
By implementing these methods, we can make our objects behave more like native types.
