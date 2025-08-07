#  Django Project & App Structure – Complete Developer Guide

This guide walks you through the structure of a Django project and app, explaining how to set it up and what each part does.

---

##  Objective

Understand how to:
- Create and structure a Django project
- Create and register apps
- Work with `settings.py`, `urls.py`, `models.py`, `views.py`
- Use templates, static files, and admin panel
- Organize everything cleanly

---

##  1. Creating the Django Project

```bash
django-admin startproject myproject
```

### Folder Structure

```
myproject/
├── manage.py
└── myproject/
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    ├── asgi.py
    └── wsgi.py
```

---

##  2. Creating a Django App

```bash
python manage.py startapp myapp
```

### Folder Structure

```
myapp/
├── admin.py
├── apps.py
├── models.py
├── tests.py
├── views.py
├── urls.py      # Create manually
└── migrations/
```

---

##  3. Project Settings (`settings.py`)

```python
# Add app
INSTALLED_APPS = [
    ...,
    'myapp',
]

# Static and Template config
STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / 'static']

TEMPLATES = [
    {
        ...,
        'DIRS': [BASE_DIR / 'templates'],
    },
]

MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

---

##  4. Models (`models.py`)

```python
from django.db import models

class Student(models.Model):
    name = models.CharField(max_length=100)
    roll_no = models.IntegerField(unique=True)
    joined_date = models.DateField(auto_now_add=True)

    def __str__(self):
        return self.name
```

```bash
python manage.py makemigrations
python manage.py migrate
```

---

##  5. Views (`views.py`)

```python
from django.shortcuts import render
from .models import Student

def home(request):
    students = Student.objects.all()
    return render(request, 'home.html', {'students': students})
```

---

##  6. URLs

### Project-level `myproject/urls.py`

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('myapp.urls')),
]
```

### App-level `myapp/urls.py`

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
```

---

## 🖼️ 7. Templates

### Folder Structure

```
myapp/
└── templates/
    └── home.html
```

### Sample Template

```html
<!DOCTYPE html>
<html>
<head><title>Students</title></head>
<body>
    <h1>Student List</h1>
    <ul>
        {% for student in students %}
            <li>{{ student.name }} - Roll No: {{ student.roll_no }}</li>
        {% endfor %}
    </ul>
</body>
</html>
```

---

## 🎨 8. Static and Media Files

### Directory Structure

```
project/
├── static/
├── media/
```

### Serve Media in `urls.py` (development only)

```python
from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

---

## 🧑‍💻 9. Admin Panel (`admin.py`)

```python
from django.contrib import admin
from .models import Student

admin.site.register(Student)
```

```bash
python manage.py createsuperuser
```

Visit: `http://localhost:8000/admin`

---

## 🧪 10. Tests (`tests.py`)

```python
from django.test import TestCase
from .models import Student

class StudentTestCase(TestCase):
    def test_student_creation(self):
        student = Student.objects.create(name="Alice", roll_no=101)
        self.assertEqual(student.name, "Alice")
```

```bash
python manage.py test
```

---

## ✅ Summary Table

| File/Folder        | Purpose |
|--------------------|---------|
| `manage.py`        | Project management commands |
| `models.py`        | Data models (ORM) |
| `views.py`         | Business logic and data handling |
| `urls.py`          | URL routing |
| `templates/`       | HTML UI |
| `static/`          | CSS, JS, images |
| `media/`           | User-uploaded content |
| `admin.py`         | Admin site configuration |
| `tests.py`         | Unit testing |

---

## 🚀 Next Steps

- Explore Class-Based Views (CBVs)
- Implement Forms and Authentication
- Learn Django REST Framework for APIs

---

*Happy Building with Django!*
