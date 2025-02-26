# Python File Handling Techniques

This guide covers essential file handling techniques in Python, including reading, writing, appending, working with different file formats, and best practices. 

## 1. Opening a File

```python
# Traditional open-close approach
file = open('example.txt', 'w')  # Open in write mode
file.close()

# Recommended approach using context manager (auto-closes file)
with open('example.txt', 'r') as file:
    content = file.read()
    print(content)
```

## 2. Reading from a File

```python
# Read entire content
with open('example.txt', 'r') as file:
    content = file.read()
    print("Full content:\n", content)

# Read line by line
with open('example.txt', 'r') as file:
    for line in file:
        print("Line:", line.strip())

# Read all lines into a list
with open('example.txt', 'r') as file:
    lines = file.readlines()
    print("All lines:", lines)
```

## 3. Writing to a File

```python
# Write new content (overwrites existing)
with open('example.txt', 'w') as file:
    file.write("Hello, World!\n")
    file.write("This is a new line.")

# Write multiple lines
lines = ["First line\n", "Second line\n", "Third line\n"]
with open('example.txt', 'w') as file:
    file.writelines(lines)
```

## 4. Appending to a File

```python
with open('example.txt', 'a') as file:
    file.write("\nThis is appended content.")
```

## 5. File Modes

| Mode  | Description |
|-------|-------------|
| 'r'   | Read mode (default) |
| 'w'   | Write mode (overwrites existing file) |
| 'a'   | Append mode (adds to end of file) |
| 'x'   | Exclusive creation (fails if file exists) |
| 'b'   | Binary mode (e.g., 'rb' or 'wb') |
| 't'   | Text mode (default) |
| '+'   | Updating mode (read/write, e.g., 'r+') |

## 6. Advanced Techniques

### 6.1 Working with Binary Files

```python
# Copying an image file
with open('input.jpg', 'rb') as src:
    with open('output.jpg', 'wb') as dest:
        dest.write(src.read())
```

### 6.2 Using `seek()` and `tell()`

```python
with open('example.txt', 'r+') as file:
    print("Initial position:", file.tell())  # 0
    content = file.read(5)  # Read first 5 characters
    print("After reading 5 chars:", file.tell())  # 5
    file.seek(0)  # Return to start of file
    file.write("New ")  # Overwrite beginning
```

### 6.3 Handling CSV Files

```python
import csv

# Writing CSV
with open('data.csv', 'w', newline='') as file:
    writer = csv.writer(file)
    writer.writerow(['Name', 'Age', 'City'])
    writer.writerow(['Alice', 30, 'New York'])
    writer.writerow(['Bob', 25, 'London'])

# Reading CSV
with open('data.csv', 'r') as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)
```

### 6.4 Working with JSON

```python
import json

# Writing JSON
data = {'name': 'Alice', 'age': 30, 'city': 'New York'}
with open('data.json', 'w') as file:
    json.dump(data, file, indent=2)

# Reading JSON
with open('data.json', 'r') as file:
    loaded_data = json.load(file)
    print(loaded_data)
```

### 6.5 Exception Handling

```python
try:
    with open('nonexistent.txt', 'r') as file:
        content = file.read()
except FileNotFoundError:
    print("Error: File not found!")
except IOError as e:
    print(f"IO Error occurred: {str(e)}")
```

### 6.6 File Path Handling (Using `pathlib`)

```python
from pathlib import Path

# Create Path object
file_path = Path('example.txt')

# Check existence
if file_path.exists():
    print("File exists!")
    
# Read content using pathlib
content = file_path.read_text()
print(content)

# Write content using pathlib
file_path.write_text("New content using pathlib")
```

## 7. Best Practices

- Always use context managers (`with` statement) for automatic resource cleanup.
- Handle exceptions properly.
- Specify encoding when working with text files (`encoding='utf-8'`).
- Use absolute paths for better portability.
- Close files explicitly when not using context managers.
- Use appropriate modes for different operations.
