# Connecting MySQL with Python - A Detailed Guide

## 📌 Introduction
Integrating MySQL with Python allows developers to create powerful database-driven applications. In this guide, we'll use the popular `mysql-connector-python` library to connect and interact with MySQL databases.

This lecture covers:
- Installing the connector
- Connecting to MySQL
- Creating databases and tables
- Inserting, reading, updating, and deleting data (CRUD)
- Using placeholders (to prevent SQL injection)
- Best practices and tips

---

## 🛠️ 1. Installing the Connector
To connect MySQL with Python, install the **MySQL Connector/Python** package:

```bash
pip install mysql-connector-python
```

You can verify the installation:
```bash
pip show mysql-connector-python
```

---

## 🔌 2. Connecting to the Database
```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="yourusername",
    password="yourpassword"
)

print(mydb)
```

If the connection is successful, you’ll see something like:
```
<mysql.connector.connection.MySQLConnection object at 0x...>
```

---

## 🧱 3. Creating a Database
```python
import mysql.connector

mydb = mysql.connector.connect(
    host="localhost",
    user="root",
    password="password"
)

mycursor = mydb.cursor()
mycursor.execute("CREATE DATABASE school")
```

To check all databases:
```python
mycursor.execute("SHOW DATABASES")
for db in mycursor:
    print(db)
```

---

## 📋 4. Creating a Table
```python
mydb = mysql.connector.connect(
    host="localhost",
    user="root",
    password="password",
    database="school"
)

mycursor = mydb.cursor()

mycursor.execute("""
CREATE TABLE students (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    age INT,
    grade VARCHAR(5)
)
""")
```

---

## 🧑‍🎓 5. Inserting Data
### Without Placeholder (Not Safe)
```python
mycursor.execute("INSERT INTO students (name, age, grade) VALUES ('Alice', 20, 'A')")
mydb.commit()
```

### With Placeholder (Safe ✅)
```python
sql = "INSERT INTO students (name, age, grade) VALUES (%s, %s, %s)"
val = ("Bob", 22, "B")
mycursor.execute(sql, val)
mydb.commit()
```

---

## 📖 6. Reading Data (SELECT)
```python
mycursor.execute("SELECT * FROM students")
result = mycursor.fetchall()

for row in result:
    print(row)
```

Read with conditions:
```python
sql = "SELECT * FROM students WHERE grade = %s"
val = ("A",)
mycursor.execute(sql, val)
for row in mycursor:
    print(row)
```

---

## ♻️ 7. Updating Data
```python
sql = "UPDATE students SET age = %s WHERE name = %s"
val = (21, "Alice")
mycursor.execute(sql, val)
mydb.commit()

print(mycursor.rowcount, "record(s) updated")
```

---

## ❌ 8. Deleting Data
```python
sql = "DELETE FROM students WHERE name = %s"
val = ("Bob",)
mycursor.execute(sql, val)
mydb.commit()

print(mycursor.rowcount, "record(s) deleted")
```

---

## 🔁 9. Looping Through Records
```python
mycursor.execute("SELECT name, grade FROM students")

for (name, grade) in mycursor:
    print(f"{name} scored {grade}")
```

---

## ✅ 10. Best Practices
- Always use placeholders to prevent SQL injection
- Use `commit()` after `INSERT`, `UPDATE`, and `DELETE`
- Use `try-except` blocks for error handling
- Close connection when done: `mydb.close()`

```python
try:
    mydb = mysql.connector.connect(
        host="localhost",
        user="root",
        password="password",
        database="school"
    )
    cursor = mydb.cursor()
    cursor.execute("SELECT * FROM students")
    for row in cursor:
        print(row)
except mysql.connector.Error as err:
    print("Error:", err)
finally:
    if mydb.is_connected():
        cursor.close()
        mydb.close()
```

---

## 🎯 Conclusion
Now you're equipped to:
- Connect Python to MySQL
- Create databases and tables
- Perform all CRUD operations
- Follow secure and efficient practices

🔍 Want to build a full project using this? Try creating a **Student Management System**!

Let me know if you want a template project for it. 🚀
