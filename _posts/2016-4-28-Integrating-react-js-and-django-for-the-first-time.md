---
layout: post
title: Basic tutorial on setting up a very basic Django and React JS application
tags: django, react, html, work
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
