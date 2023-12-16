---
layout: post
title: "Django"
category: jekyll update
---

A web development framework for backend operations with batteries included - 

- admin site
- ORM mapper
- authentication
- caching

## Setting up & Creating Project

### Install Django using pipenv
{% highlight shell %}
pip3 install pipenv
mkdir ~/storeFront && cd ~/storeFront
pipenv install django

# to activate the virtual environment
pipenv shell
{% endhighlight %}

### Create Django project
{% highlight shell %}
django-admin startproject storeFront .
{% endhighlight %}

### The directory structure
{% highlight shell %}
storeFront/
  storeFront/
    __init.py__
    asgi.py
    settings.py
    urls.py
    wsgi.py
  manage.py
{% endhighlight %}

## Creating apps
A Django app is a web application that does a particular job. It can live anywhere in the Python path. A Django project can consist of multiple apps and an app can be used in multiple projects. They can be distributed also to be used by others - 

{% highlight python %}
python manage.py startapp playground

# add the app in the settings file
...
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    ...
    'playground'
]
{% endhighlight %}

### The directory structure
{% highlight python %}
playground
  migrations/
  __init.py__
  admin.py
  apps.py
  models.py
  tests.py
  views.py
{% endhighlight %}

## Views
Views can be considered as request handler.
{% highlight python %}
from django.http import HttpResponse

def say_hello(request):
  return HttpResponse('Hello World!')
{% endhighlight %}

### Generic View

## URLconf
To call a view we need to map it to a url and it can be done using `URLconf`.
{% highlight python %}
# in app urls.py

from django.urls import path
from . import views

urlpatterns = [
  path('hello/', views.say_hello)
]

# in project urls.py

from django.urls import path, include

urlpatterns = [
  path('admin/', admin.site.urls),
  path('playground/', include('playground.urls'))
]
{% endhighlight %}

always end urls with forward-slash (/)

### path()
`path()`` function has the following parameters - 

- route - str. It specifies the url pattern. When processing a request Django match from top to bottom in a urlpatterns. Also GET and POST or the domain name are not mathced.
- view - 
- kwargs - 
- name

## Models
{% highlight bash %}
python manage.py makemigrations
python manage.py sqlmigrate storeFront 0001
python manage.py migrate
{% endhighlight %}

`migrate`` command check INSTALLED_APPS and create any necessary tables in the database mentioned in the  database settings specified in settings.py.
- The table name is created by `<name of the app>_<lowercase name of the model>`
- `id` field is auto added and made as primary key unless otherwise stated
- `_id` is appended to foreign key by default

## Templates
Default settings create a DjangoTemplates backend whose APP_DIRS is set to true. Therefore Django looks inside each templates subdirectory under each INSTALLED_APPS.

### Rendering Templates

{% highlight python %}
from django.http import HttpResponse
from django.shortcuts import render
from django.templates import loader

def say_hello(request):
...
  return HttpResponse("Hello World")
  
  template = loader('polls/index.html')
  return HttpResponse(template.render({'name': 'nakib'} ,request))
  
  reutrn render(request, 'polls/index.html', {'name': 'nakib'})
{% endhighlight %}

### Templates
Django do a dot-lookup syntax for accessing variable attribute. [django lookup](Django dot-lookup syntax to access variable attributes)
- `\{\{ }}`
- `\{\% if %} ... \{\% else \%\} ... \{\%endif\%\}`
- `\{\% for \%\} ... \{\% endfor \%\}`
- `\{\% url \%\}`
- `\{\% load \%\}`
- `\{\% static \%\}`

## Debugging
- Using VSCode
- Django Debug Toolbar

## Admin
{% highlight python %}
python manage.py createsuperuser
{% endhighlight %}

Register your apps in admin -
{% highlight python %}
# in polls/admin.py
from . import models

admin.site.register(models.Question)
{% endhighlight %}

## Tests

[django lookup]: https://stackoverflow.com/questions/32767629/django-dot-lookup-syntax-to-access-variable-attributes