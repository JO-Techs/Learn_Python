# Python Data Structures

This guide covers the fundamental data structures in Python, including lists, tuples, sets, dictionaries, and more, with practical examples.

## 1. Lists

Lists are ordered, mutable collections that allow duplicate elements.

```python
# Creating a list
my_list = [1, 2, 3, 4, 5]

# Accessing elements
print(my_list[0])  # First element
print(my_list[-1])  # Last element

# Modifying a list
my_list.append(6)  # Adding an element
my_list.remove(2)  # Removing an element

# Iterating through a list
for item in my_list:
    print(item)
```

## 2. Tuples

Tuples are ordered, immutable collections that allow duplicate elements.

```python
# Creating a tuple
my_tuple = (1, 2, 3, 4, 5)

# Accessing elements
print(my_tuple[1])  # Second element

# Tuples are immutable, so elements cannot be changed
```

## 3. Sets

Sets are unordered, mutable collections that do not allow duplicate elements.

```python
# Creating a set
my_set = {1, 2, 3, 4, 5}

# Adding and removing elements
my_set.add(6)
my_set.remove(3)

# Set operations
set1 = {1, 2, 3}
set2 = {3, 4, 5}
print(set1.union(set2))  # {1, 2, 3, 4, 5}
print(set1.intersection(set2))  # {3}
```

## 4. Dictionaries

Dictionaries are key-value pairs that allow efficient lookups.

```python
# Creating a dictionary
my_dict = {'name': 'Alice', 'age': 25, 'city': 'New York'}

# Accessing values
print(my_dict['name'])

# Modifying dictionary
my_dict['age'] = 26
my_dict['job'] = 'Engineer'

# Iterating through dictionary
for key, value in my_dict.items():
    print(f"{key}: {value}")
```

## 5. Stacks (Using Lists)

Stacks follow the LIFO (Last In, First Out) principle.

```python
# Implementing a stack
stack = []
stack.append(1)
stack.append(2)
stack.append(3)
print(stack.pop())  # Removes 3 (last in, first out)
```

## 6. Queues (Using Collections)

Queues follow the FIFO (First In, First Out) principle.

```python
from collections import deque

# Implementing a queue
queue = deque()
queue.append(1)
queue.append(2)
queue.append(3)
print(queue.popleft())  # Removes 1 (first in, first out)
```

## 7. Linked Lists (Using Classes)

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def append(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return
        temp = self.head
        while temp.next:
            temp = temp.next
        temp.next = new_node

    def print_list(self):
        temp = self.head
        while temp:
            print(temp.data, end=' -> ')
            temp = temp.next
        print('None')

# Usage
ll = LinkedList()
ll.append(1)
ll.append(2)
ll.append(3)
ll.print_list()
```

## 8. Heap (Using Heapq)

Heaps are used for priority queues.

```python
import heapq

# Creating a min-heap
heap = []
heapq.heappush(heap, 3)
heapq.heappush(heap, 1)
heapq.heappush(heap, 2)
print(heapq.heappop(heap))  # Removes smallest element (1)
```

## 9. Graphs (Using Dictionaries)

```python
# Graph representation using adjacency list
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D', 'E'],
    'C': ['A', 'F'],
    'D': ['B'],
    'E': ['B', 'F'],
    'F': ['C', 'E']
}

# Traversing the graph using BFS
from collections import deque

def bfs(start):
    visited = set()
    queue = deque([start])
    while queue:
        node = queue.popleft()
        if node not in visited:
            print(node, end=' ')
            visited.add(node)
            queue.extend(graph[node])

bfs('A')
```

## 10. Best Practices

- Lists = dynamic arrays.
- Tuples when immutability is required.
- Sets = unique element storage and set operations.
- Dictionaries = fast lookups and key-value mapping.
- Use `collections.deque` for efficient queue operations.
- Use `heapq` for priority queue operations.

