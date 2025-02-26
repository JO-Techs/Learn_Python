# Object Oriented Programming in Python

This guide explores object-oriented programming (OOP) concepts in Python, including inheritance, polymorphism, abstract classes, metaclasses, and more.

## 1. Class Methods and Static Methods

### Class Methods (`@classmethod`)
Class methods take the class as the first parameter and can modify class variables.

```python
class MyClass:
    class_variable = 0
    
    def __init__(self, value):
        self.value = value
    
    @classmethod
    def increment_class_variable(cls):
        cls.class_variable += 1

MyClass.increment_class_variable()
print(MyClass.class_variable)  # Output: 1
```

### Static Methods (`@staticmethod`)
Static methods do not modify class state and act like normal functions inside a class.

```python
class MathOperations:
    @staticmethod
    def add(a, b):
        return a + b

print(MathOperations.add(3, 5))  # Output: 8
```

## 2. Multiple Inheritance
A class can inherit from multiple base classes.

```python
class A:
    def show(self):
        print("A")

class B:
    def display(self):
        print("B")

class C(A, B):
    pass

obj = C()
obj.show()  # Output: A
obj.display()  # Output: B
```

## 3. Method Resolution Order (MRO)
Python follows the C3 linearization algorithm (depth-first, left-to-right order).

```python
class A:
    def show(self):
        print("A")

class B(A):
    def show(self):
        print("B")

class C(A):
    def show(self):
        print("C")

class D(B, C):
    pass

obj = D()
obj.show()  # Output: B (MRO: D -> B -> C -> A)
```

## 4. Abstract Classes (`abc` Module)
Abstract classes enforce method implementation in subclasses.

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def make_sound(self):
        pass

class Dog(Animal):
    def make_sound(self):
        return "Bark"

d = Dog()
print(d.make_sound())  # Output: Bark
```

## 5. Properties and Getters/Setters
Using `property` to define getters and setters.

```python
class Person:
    def __init__(self, name):
        self._name = name

    @property
    def name(self):
        return self._name

    @name.setter
    def name(self, new_name):
        if isinstance(new_name, str) and len(new_name) > 0:
            self._name = new_name
        else:
            raise ValueError("Invalid name")

p = Person("Alice")
p.name = "Bob"
print(p.name)  # Output: Bob
```

## 6. Operator Overloading
Redefining operators for user-defined classes.

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)
    
    def __str__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(2, 3)
v2 = Vector(1, 5)
v3 = v1 + v2
print(v3)  # Output: Vector(3, 8)
```

## 7. Metaclasses
Metaclasses allow customization of class creation.

```python
class Meta(type):
    def __new__(cls, name, bases, dct):
        dct['new_attribute'] = 'Added via metaclass'
        return super().__new__(cls, name, bases, dct)

class MyClass(metaclass=Meta):
    pass

print(MyClass.new_attribute)  # Output: Added via metaclass
```

## 8. Object Introspection
Examining an object’s attributes and methods at runtime.

```python
class Test:
    def method(self):
        pass

obj = Test()
print(dir(obj))  # Lists all attributes and methods
print(hasattr(obj, 'method'))  # Output: True
print(callable(getattr(obj, 'method', None)))  # Output: True
```

## 9. Singleton Pattern
Ensuring only one instance of a class exists.

```python
class Singleton:
    _instance = None
    
    def __new__(cls):
        if cls._instance is None:
            cls._instance = super(Singleton, cls).__new__(cls)
        return cls._instance

s1 = Singleton()
s2 = Singleton()
print(s1 is s2)  # Output: True
```

## 10. Best Practices
- Use abstract base classes to enforce method implementation.
- Prefer composition over inheritance when appropriate.
- Use `property` for controlled attribute access.
- Use metaclasses only when necessary.
- Follow the principle of encapsulation by keeping attributes private when necessary.
