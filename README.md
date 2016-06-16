# django-guide
Guide to get you started with Django with minimal effort, as soon as possible.

![django-guide](img/django.jpg)

## Contents
1. [History](#history)
2. 
[Running A Server](#running-a-server)

## History

Alright, some history of Django- In summer 2005, after having developed this framework to a point where it was efficiently powering most of World Online’s sites, the World Online team, which now included Jacob Kaplan-Moss, decided to release the framework as open source software. They released it in July 2005 and named it Django, after the jazz guitarist Django Reinhardt.

Django’s origins have shaped the culture of its open source community. Because Django was extracted from real-world code, rather than being an academic exercise or commercial product, it is acutely focused on solving Web development problems that Django’s developers themselves have faced — and continue to face. As a result, Django itself is actively improved on an almost daily basis. The framework’s developers have a keen interest in making sure Django saves developers time, produces applications that are easy to maintain, and performs well under load. If nothing else, the developers are motivated by their own selfish desires to save themselves time and enjoy their jobs. (To put it bluntly, they eat their own dog food.) (Source: thedjangobook.com)

## Running a server

-> Running a server in default mode, it's most probably set to 127.0.0.1:8000, that's where you can access it via a web browser.

```
$python manage.py runserver
```

-> Running a server at a specific port, say you're running another application on the present server, you can run your project's server at a port you specified by supplying it as an argument.

```
python manage.py runserver 3000

#Django version 1.10a1, using settings 'mysite.settings'
#Starting development server at http://127.0.0.1:3000/
#Quit the server with CONTROL-C.
```
