# Python Data Structures: List, Tuple, and Dictionary Functions

## 1. List Methods
### What?
A list is a mutable sequence used to store a collection of items.

### Common List Methods:
```python
# Creating a list
my_list = [1, 2, 3, 4, 5]

# Adding elements
my_list.append(6)       # Adds an element to the end
my_list.insert(2, 99)   # Inserts 99 at index 2

# Removing elements
my_list.remove(3)       # Removes the first occurrence of 3
popped = my_list.pop()  # Removes and returns the last element

# Finding elements
index = my_list.index(99)  # Finds the index of 99
count = my_list.count(2)   # Counts occurrences of 2

# Sorting and reversing
my_list.sort()       # Sorts the list in ascending order
my_list.reverse()    # Reverses the list

# Copying and clearing
copy_list = my_list.copy()  # Creates a copy of the list
my_list.clear()             # Removes all elements
```

### Why Use?
- Lists are versatile and widely used for dynamic collections of items.

### Common Pitfalls:
- Using `remove()` without checking if the element exists.
- Mutating a list while iterating over it.

---

## 2. Tuple Methods
### What?
A tuple is an immutable sequence used to store a collection of items.

### Common Tuple Methods:
```python
# Creating a tuple
tuple1 = (1, 2, 3, 4, 5)

# Accessing elements
first_element = tuple1[0]   # Access first element
sliced_tuple = tuple1[1:3]  # Slicing a tuple

# Finding elements
index = tuple1.index(3)  # Finds the index of 3
count = tuple1.count(2)  # Counts occurrences of 2
```

### Why Use?
- Tuples are faster and more memory-efficient than lists.
- Useful for fixed collections of data.

### Common Pitfalls:
- Attempting to modify a tuple (tuples are immutable).

---

## 3. Dictionary Methods
### What?
A dictionary is an unordered collection of key-value pairs.

### Common Dictionary Methods:
```python
# Creating a dictionary
my_dict = {"name": "Alice", "age": 25, "city": "New York"}

# Adding and updating values
my_dict["age"] = 26        # Updating a value
my_dict["country"] = "USA" # Adding a new key-value pair

# Removing elements
del my_dict["city"]        # Deletes a key-value pair
removed_value = my_dict.pop("age")  # Removes key and returns value
my_dict.clear()             # Removes all items

# Accessing values
value = my_dict.get("name")  # Returns value for key, or None if not found
keys = my_dict.keys()        # Returns a view of all keys
values = my_dict.values()    # Returns a view of all values
items = my_dict.items()      # Returns a view of key-value pairs

# Copying a dictionary
copy_dict = my_dict.copy()  # Creates a copy of the dictionary
```

### Why Use?
- Efficient key-value storage and lookup.
- Ideal for structured data representation.

### Common Pitfalls:
- Trying to access a missing key without using `.get()`.
- Modifying a dictionary while iterating over it.

---

## Summary of Methods

| Structure  | Method         | Description |
|------------|---------------|-------------|
| **List**  | `.append(x)`   | Adds x to the end |
|           | `.insert(i, x)` | Inserts x at index i |
|           | `.remove(x)`   | Removes the first occurrence of x |
|           | `.pop(i)`      | Removes and returns element at index i (default: last) |
|           | `.sort()`      | Sorts the list in ascending order |
|           | `.reverse()`   | Reverses the list |
|           | `.copy()`      | Returns a shallow copy |
|           | `.clear()`     | Removes all elements |
| **Tuple** | `.count(x)`    | Returns the count of x |
|           | `.index(x)`    | Returns the index of x |
| **Dictionary** | `.get(key)`   | Returns value for key, or None if missing |
|           | `.pop(key)`    | Removes key and returns its value |
|           | `.keys()`      | Returns all keys |
|           | `.values()`    | Returns all values |
|           | `.items()`     | Returns all key-value pairs |
|           | `.copy()`      | Returns a shallow copy |
|           | `.clear()`     | Removes all items |

This guide covers the most essential functions of lists, tuples, and dictionaries in Python.
