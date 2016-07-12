# django-guide
Guide to get you started with Django with minimal effort, as soon as possible.

![django-guide](img/django.jpg)

## Contents
[History](#history)

[Installing Python](#installing-python)

[Virtual Environment](#virtual-environment)

[Running A Server](#running-a-server)

[Setting up MySQL](#setting-up-mysql)

[Setting up Static Files](#setting-up-static-files)

[Setting up Template directories](#setting-up-template-directories)



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


## Virtual Environment

### Installing a Virtual Environment
```python
pip install virtualenv
```
### Setting up a virtual environment
```python
virtualenv myNewProject
#starts a new project folder with the name 'myNewProject'
```
### Running the virtual environment
```python
#cd into the folder and type
source bin/activate
#This should enter you into the virutual environment
```
### Check your django dependencies (installed)
```python
pip freeze

Django==1.9.7
PAM==0.4.2
Pillow==2.3.0
Twisted-Core==13.2.0
Twisted-Web==13.2.0
apt-xapian-index==0.45
argparse==1.2.1
beautifulsoup4==4.2.1
chardet==2.0.1
colorama==0.2.5
command-not-found==0.3
configobj==4.7.2
debtagshw==0.1
...
```
### Packaging Django dependencies to requirements.txt file
```python
# Go to root of your virtualenv and type
pip freeze > requirements.txt
```
### Installing Django dependencies in your virtualenv project
```python
# go to root of django virtualenv path and type
pip install requirements.txt
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
#views.py

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

Add a context that needs to be rendered in a template, first we write some Django template code in a html file.

```html
<!DOCTYPE html>
<html>
<head>
	<title>Index</title>
</head>
<body>
<h1>This is a template! </h1>
<p>{{name}}, Welcome to my website</p>
</body>
</html>
```
And then a context that needs to replace placeholder variables in the template.

```python
#views.py
from django.http import HttpResponse
from django.shortcuts import render

def url1(request):
	context= {"name":"Pranay"}
	template = "index.html"
	return render(request,template,context)
```

## Setting Up MySQL

```python
sudo apt-get install python-dev python3-dev
sudo apt-get install libmysqlclient-dev
pip install MySQL-python
pip install pymysql
pip install mysqlclient

#http://stackoverflow.com/questions/19189813/setting-django-up-to-use-mysql
```

#### Creating a database
Create a database in mysql console and update the name of the database in settings.py
```python
#refer to this link
# http://stackoverflow.com/questions/24462007/how-to-deal-with-this-error-1049-unknown-database-users-ohyunjun-work-astra
```
## Setting up static files

Add the following to settings.py
```python
STATIC_URL = '/static/'

# the static folder of the django project must be placed in the root(where the manage.py file lies)
STATICFILES_DIRS = (
    os.path.join(BASE_DIR,'static'),# don't forget the trailing comma
)
```

## Setting up Template directories
```python
# Python automatically detects the 'template' folders in respective apps,
# you can simply use render(request,'index.html',{}) - where index.html is located in app/templates/index.html
```

Misc
Setting up template directory - http://stackoverflow.com/questions/3038459/django-template-path
Suppose you wanted a template directory for the root app, add the path.join(BASE_DIR, 'template'),
refer this for better understanding http://stackoverflow.com/questions/3038459/django-template-path
