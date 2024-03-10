**Title: Building a Django Todo App**

**Summary:**  
we will guide you through the process of creating a Django Todo App. By following along, you'll learn how to set up a virtual environment, install Django, create a new project, handle static files and templates, create a todo app, define models, apply migrations, and more.

---

### **Step 1: Setting Up Your Environment**

#### **1.1 Creating a Virtual Environment**

```bash
python -m venv venv
```

Activate the virtual environment:

```bash
venv\scripts\activate  # For Windows
source venv/bin/activate  # For macOS and Linux
```

#### **1.2 Installing Django**

```bash
pip install django
```

### **Step 2: Creating Your Project**

#### **2.1 Starting a New Project**

```bash
django-admin startproject todo_list
```

### **Step 3: Managing Static Files**

#### **3.1 Configuring Static Files**

```bash
mkdir static
```

Update `settings.py`:

```python
STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / 'static']
```

### **Step 4: Handling Templates**

#### **4.1 Creating Templates**

```bash
mkdir templates
```

Define `base.html` in the templates directory.

#### **4.2 Configuring Templates**

Update `settings.py`:

```python
'DIRS': [BASE_DIR / 'templates' ],
```

### **Step 5: Creating the Todo App**

#### **5.1 Setting Up the App**

```bash
django-admin startapp todo
```

Add `'todo',` to `INSTALLED_APPS` in `settings.py`.

#### **5.2 Defining Views**

Create a `views.py` file in the `todo` app:

```python
from django.shortcuts import render

def home(request):
    return render(request, 'home.html')
```

#### **5.3 Routing URLs**

Define URL routes in `urls.py`:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
```

Include the app's URLs in the project's `urls.py`:

```python
path('', include('todo.urls'))
```

### **Step 6: Creating the Task Model**

#### **6.1 Defining the Model**

Define the `Task` model in `models.py`:

```python
from django.db import models
from django.contrib.auth.models import User

class Task(models.Model):
    title = models.CharField(max_length=255)
    description = models.TextField(null=True, blank=True)
    completed = models.BooleanField(default=False)
    created_at = models.DateTimeField(auto_now_add=True)
    user = models.ForeignKey(User, on_delete=models.CASCADE, null=True, blank=True)
    
    def __str__(self):
        return self.title
    
    class Meta:
        ordering = ['completed']
```

#### **6.2 Registering the Model in Admin**

Register the `Task` model in `admin.py`:

```python
from django.contrib import admin
from .models import Task

admin.site.register(Task)
```

#### **6.3 Applying Migrations**

```bash
python manage.py makemigrations
python manage.py migrate
```

#### **6.4 Creating a Superuser**

```bash
python manage.py createsuperuser
```

### **Step 7: Finalizing and Testing**

Restart the Django server:

```bash
python manage.py runserver
```

Navigate to `http://127.0.0.1:8000/` in your web browser.

---
