# django-guide
Guide to get you started with Django with minimal effort, as soon as possible.

![django-guide](img/django.jpg)

## Contents
[History](#history)

[Installing Python](#installing-python)

[Running A Server](#running-a-server)

## History

Alright, some history of Django- In summer 2005, after having developed this framework to a point where it was efficiently powering most of World Online’s sites, the World Online team, which now included Jacob Kaplan-Moss, decided to release the framework as open source software. They released it in July 2005 and named it Django, after the jazz guitarist Django Reinhardt.

Django’s origins have shaped the culture of its open source community. Because Django was extracted from real-world code, rather than being an academic exercise or commercial product, it is acutely focused on solving Web development problems that Django’s developers themselves have faced — and continue to face. As a result, Django itself is actively improved on an almost daily basis. The framework’s developers have a keen interest in making sure Django saves developers time, produces applications that are easy to maintain, and performs well under load. If nothing else, the developers are motivated by their own selfish desires to save themselves time and enjoy their jobs. (To put it bluntly, they eat their own dog food.) (Source: thedjangobook.com)

## Installing Python

### Windows 
[Windows Executables](https://www.python.org/downloads/windows/)

### Mac OS 
[Mac](https://www.python.org/downloads/mac-osx/)

### Linux
```
$ sudo apt-get install python
```

## Running a server

-> Running a server in default mode, it's most probably set to 127.0.0.1:8000, that's where you can access it via a web browser.

```
$ python manage.py runserver
```

-> Running a server at a specific port, say you're running another application on the present server, you can run your project's server at a port you specified by supplying it as an argument.

```
python manage.py runserver 3000

#Django version 1.10a1, using settings 'mysite.settings'
#Starting development server at http://127.0.0.1:3000/
#Quit the server with CONTROL-C.
```

-> Running a server with specified IP & port.

```
python manage.py runserver 0.0.0.0:3000

#Django version 1.10a1, using settings 'mysite.settings'
#Starting development server at http://0.0.0.0:3000/
#Quit the server with CONTROL-C.
```

## URLs

### How to set the homepage in django
```
url(r'^$', somefile.somemethod)
```
### Setting urlpatterns and making function based views work

```python
#urls.py
"""lenz URL Configuration

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/dev/topics/http/urls/
Examples:
Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  url(r'^$', views.home, name='home')
Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  url(r'^$', Home.as_view(), name='home')
Including another URLconf
    1. Import the include() function: from django.conf.urls import url, include
    2. Add a URL to urlpatterns:  url(r'^blog/', include('blog.urls'))
"""
from django.conf.urls import url
from django.contrib import admin
from . import views ## relative inclusion of files, this means from current directory (.) import views.py 

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^$', views.url1)
]

```

```python
from django.http import HttpResponse


def url1(request):
	return HttpResponse("<h1>This works!</h1>)
```


### Rendering templates via function based views
#### But first, we need to add template directory to your project path so django knows you have templates that you need to use, go to settings.py and edit the templates dictionary.
```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, "templates")],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```



```python
#views.py
from django.http import HttpResponse
from django.shortcuts import render

def url1(request):
	context= {"name":"Pranay"}
	template = "index.html"
	return render(request,template,context)
```
