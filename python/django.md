---
title: Django Framework
description: 
published: true
date: 2020-05-15T00:07:14.253Z
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

Start a project

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