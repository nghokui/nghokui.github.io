---
layout: post
title: Basic tutorial on setting up a very basic Django and React JS application
tags: django, react, html, work
---

## 2. Set up the django local server
Let's start of by doing all the things necessary to get the most basic django server running.
##### Get our main django project up and running
Let's start easy and have our urlsconf redirect to our application. If we're in the project root directory, open up `your_project_name/urls.py` and make it look like this
We're pretty much just setting up the website to send a url of http://127.0.0.1:8000/ to our `your_app_name`... err... app!

```
from django.conf.urls import include, url
...
urlpatterns = [
  url(r'^', include('your_app_name.urls')),
  url(r'^admin/', admin.site.urls),
]
```

Now time to set up our `your_project_name/settings.py` file. Open it up and let's add some stuff.
I'm only going to show things that I'm adding around what's already there

```
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

Now, let's set up our django app. Let's first open up our `your_project_name/your_app_name/urls.py` and let's handle the url passing.
Since we're going to assume that the home page (`http://127.0.0.1:8000`, the default django server port) is going to direct to this app, add the following

```
from django.conf.urls import url
from . import views

urlpatterns = [
  url(r'^', views.index, name='index'),
]
```
This will allow us to return a view specified in our `your_app_name/views.py` file. Now on to that...

Open up `your_app_name/views.py` and let's create the view that's going to display. Well, sans-html of course. We'll get to that real soon.

```
def index(request):
  return render(request, 'your_app_name/index.html', { })
```
Alright! So now we're returning a view. Well... an empty html file....

So let's fix the html file! Let's put some super simple html
```
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
