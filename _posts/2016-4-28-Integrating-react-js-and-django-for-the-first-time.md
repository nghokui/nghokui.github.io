---
layout: post
title: Starting off my fantasy football web application
tags: django, mysql, fantasy football
---
Setting up a basic app with ReactJS and Django

## 0. [Pre-step] Install Node.js and Django
If not installed already, we'll need to install Node.js [here](https://nodejs.org/en/download/) and django can be installed with
```python
$ pip install django
```
This, of course, assumes python is already installed (why haven't you already!)


## 1. Initialize the project directory
A few things we need to initialize:
##### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Build the backend stuff (Django)
1. Create the Django project and navigate into project root directory
```
$ cd /path/to/directory/
$ django-admin startproject your_project_name
$ cd your_project_name
```
2. Create an app within our Django project
```
$ python manage.py startapp your_app_name
```
While we're here, let's create some files and directories inside our app
  * Create templates and static directories
```
$ mkdir your_app_name/static/your_app_name
$ mkdir your_app_name/templates/your_app_name
```
  * Create our files (that we'll edit later)
```
$ touch your_app_name/urls.py
$ touch your_app_name/templates/your_app_name/index.html
```

##### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Build the frontend stuff (the stuff we'll need for ReactJS)
1. Initialize the node.js package (this generates our package.json file)
```
$ npm init
```
2. ... and of course we'll need to install our dependencies
```
$ npm install --save-dev react react-dom webpack webpack-bundle-tracker babel babel-loader babel-preset-react
```
3. Let's create our folders and files that we'll need to play with webpack
```
$ mkdir -p assets/js
$ touch webpack.config.js
$ touch assets/js/index.js
```

## 2. Set up the django local server
Let's start of by doing all the things necessary to get the most basic django server running.
##### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Get our main django project up and running
1. Let's start easy and have our urlsconf redirect to our application. If we're in the project root directory, open up `your_project_name/urls.py` and make it look like this
We're pretty much just setting up the website to send a url of http://127.0.0.1:8000/ to our `your_app_name`... err... app!
``` python
from django.conf.urls import include, url
...
urlpatterns = [
  url(r'^', include('your_app_name.urls')),
  url(r'^admin/', admin.site.urls),
]
```
Awesome.
2. Now time to set up our `your_project_name/settings.py` file. Open it up and let's add some stuff.
I'm only going to show things that I'm adding around what's already there
``` python
INSTALLED_APPS = [
  'your_app_name.apps.Your_app_nameConfig', # we're adding our app to the installed apps list
  ...
]
...
# all the way at the bottom of the page let's add..
STATIC_ROOT = ''
STATICFILES_DIRS = (os.path.join('static'),)
```
Fantastic!
3. Now, let's set up our django app. Let's first open up our `your_project_name/your_app_name/urls.py` and let's handle the url passing.
Since we're going to assume that the home page (`http://127.0.0.1:8000`, the default django server port) is going to direct to this app, add the following
``` python
from django.conf.urls import url
from . import views

urlpatterns = [
  url(r'^', views.index, name='index'),
]
```
This will allow us to return a view specified in our `your_app_name/views.py` file. Now on to that...
4. Open up `your_app_name/views.py` and let's create the view that's going to display. Well, sans-html of course. We'll get to that real soon.

``` python
def index(request):
  return render(request, 'your_app_name/index.html', {})
```
Alright! So now we're returning a view. Well... an empty html file....
5. So let's fix the html file! Let's put some super simple html
``` html
{% load static %}
<!DOCTYPE html>
<html>
    <head>
      <meta charset="UTF-8">
      <title>Let's get React and Django to play nicely</title>
    </head>
    <body>
      <div id="app"></div>
      <script src="{% static "your_app_name/bundle.js" %}"></script>
    </body>
</html>
```
A few things in this html file:
* `<div id="app">` is where we're going to have the react hook in.
* `{% load static %}` ... `<script src="{% static "your_app_name/bundle.js" %}"></script>` is where we'll import our React code.
Awesome!
6. Let's try out our server!

At this point, we can actually run our server and see what happens. If we just get a blank page returned, we know we're golden (and no errors when our server is started).
So, that being said:
```
$ python manage.py migrate
$ python manage.py runserver
```
I think we're rolling along swimmingly! Just note: the migrate command isn't totally necessary at this point in time (since we didn't make any database models), but I
just like to get rid of the warning. Let's `Command + c` or `Ctrl + c` out of there and move on to getting our react stuff all set up.
