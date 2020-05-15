---
title: Django Framework
description: 
published: true
date: 2020-05-15T21:30:27.548Z
tags: django, python, framework
---

# Installation

Enable venv

```
python3.7 -m venv django-project
source django-project/bin/activate
pip install Django
```

Check version

```
python -m django --version
3.0.6
```

# Start a project

```
django-admin startproject jarlok .
python manage.py migrate
```

Create application



```
python manage.py startapp pages
```


Modify

```
# pages/views.py
from django.http import HttpResponse


def homePageView(request):
    return HttpResponse('Hello, World!')
```

Create

```
# pages/urls.py
from django.urls import path

from .views import homePageView

urlpatterns = [
    path('', homePageView, name='home')
]
```

Update
```
# jarlok/urls.py
from django.contrib import admin
from django.urls import path, include # new

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('pages.urls')), # new
]
```


```
$ tree   
.                                                     
├── db.sqlite3                                        
├── jarlok                                            
│   ├── asgi.py                                       
│   ├── __init__.py                                   
│   ├── __pycache__                                   
│   │   ├── __init__.cpython-37.pyc                   
│   │   ├── settings.cpython-37.pyc                   
│   │   ├── urls.cpython-37.pyc                       
│   │   └── wsgi.cpython-37.pyc                       
│   ├── settings.py                                   
│   ├── urls.py                                       
│   └── wsgi.py                                       
├── manage.py                                         
└── pages                                             
    ├── admin.py                                      
    ├── apps.py                                       
    ├── __init__.py                                   
    ├── migrations                                    
    │   └── __init__.py                               
    ├── models.py                                     
    ├── __pycache__                                   
    │   ├── __init__.cpython-37.pyc                   
    │   ├── urls.cpython-37.pyc                       
    │   └── views.cpython-37.pyc                      
    ├── tests.py                                      
    ├── urls.py                                       
    └── views.py                                      
                                                      
```

Run
```
$ python manage.py runserver
```

Check
```
 http://127.0.0.1:8000/ 
 ```
 
 # Start JWT (JSON Web Token) project
 
 
```
pip install django
pip install djangorestframework
pip install django-cors-headers
pip install djangorestframework-jwt
```

Create django project

```
django-admin.py startproject myProj .
```
Go to project and create app
```
cd myProj
django-admin.py startapp myapp

$ tree

myProj/
 |-- myapp/
 |    |-- migrations/
 |    |-- __init__.py
 |    |-- admin.py
 |    |-- apps.py
 |    |-- models.py
 |    |-- tests.py
 |    +-- views.py
 |-- __init__.py
 |-- settings.py
 |-- urls.py
 +-- wsgi.py
manage.py
```

In the `settings.py` file, add the following configurations:

```
REST_FRAMEWORK = {
  'DEFAULT_AUTHENTICATION_CLASSES': (
    'rest_framework_jwt.authentication.JSONWebTokenAuthentication',
  ),
}
```

Database:

```
$ sudo apt-get install postgresql postgresql-contrib postgresql-server-dev-11
$ sudo su postgres
$ psql

postgres=# create database mydatabase;
CREATE DATABASE
postgres=# CREATE ROLE myuser WITH LOGIN PASSWORD 'seronoser';
CREATE ROLE
postgres=# grant ALL PRIVILEGES ON DATABASE mydatabase TO myuser;
GRANT
postgres=# 
```

Install the `psycopg2` package, which will allow us to use the database we configured:

```
pip install wheel
pip install psycopg2
```

Edit `settings.py`

Remove this
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```
And add this
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'mydatabase',
        'USER': 'myuser',
        'PASSWORD': 'seronoser',
        'HOST': 'localhost',
        'PORT': '',
    }
}
```

Edit `models.py` like this:

```py
# users/models.py
from __future__ import unicode_literals
from django.db import models, transaction
from django.utils import timezone
from django.contrib.auth.models import (
    AbstractBaseUser, PermissionsMixin, BaseUserManager
)


class UserManager(BaseUserManager):

    def _create_user(self, email, password, **extra_fields):
        """
        Creates and saves a User with the given email,and password.
        """
        if not email:
            raise ValueError('The given email must be set')
        try:
            with transaction.atomic():
                user = self.model(email=email, **extra_fields)
                user.set_password(password)
                user.save(using=self._db)
                return user
        except:
            raise

    def create_user(self, email, password=None, **extra_fields):
        extra_fields.setdefault('is_staff', False)
        extra_fields.setdefault('is_superuser', False)
        return self._create_user(email, password, **extra_fields)

    def create_superuser(self, email, password, **extra_fields):
        extra_fields.setdefault('is_staff', True)
        extra_fields.setdefault('is_superuser', True)

        return self._create_user(email, password=password, **extra_fields)


class User(AbstractBaseUser, PermissionsMixin):
    """
    An abstract base class implementing a fully featured User model with
    admin-compliant permissions.
 
    """
    email = models.EmailField(max_length=40, unique=True)
    first_name = models.CharField(max_length=30, blank=True)
    last_name = models.CharField(max_length=30, blank=True)
    is_active = models.BooleanField(default=True)
    is_staff = models.BooleanField(default=False)
    date_joined = models.DateTimeField(default=timezone.now)
 
    objects = UserManager()
 
    USERNAME_FIELD = 'email'
    REQUIRED_FIELDS = ['first_name', 'last_name']
 
    def save(self, *args, **kwargs):
        super(User, self).save(*args, **kwargs)
        return self
```

Edit `settings.py` and add 

```
AUTH_USER_MODEL='myProj.User'
```

In myProj directory run
```
python manage.py makemigrations myapp
python manage.py migrate
```

Tables automatically created
```
mydatabase=# \dt
                        List of relations
 Schema |             Name              | Type  |     Owner      
--------+-------------------------------+-------+----------------
 public | auth_group                    | table | gopher_backend
 public | auth_group_permissions        | table | gopher_backend
 public | auth_permission               | table | gopher_backend
 public | myapp_user                    | table | gopher_backend
 public | myapp_user_groups             | table | gopher_backend
 public | myapp_user_user_permissions   | table | gopher_backend
 public | django_admin_log              | table | gopher_backend
 public | django_content_type           | table | gopher_backend
 public | django_migrations             | table | gopher_backend
 public | django_session                | table | gopher_backend
(10 rows)
```

