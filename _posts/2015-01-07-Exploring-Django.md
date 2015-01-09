---
layout: post
title: Exploring Django
comments: True
redirect_from: "/2015/01/05/Exploring-Django/"
permalink: exploring-django
---

This post needs look at [previous post](http://kranthi.gearsystems.org/setting-up-django)
Once you are done with the runserver and you know that a server is running on your system at `localhost:8000` the following things shall help you in exploring django.Also, create a database with some name and enter that name in the DATABASE dictionary in settings.py file.

Note that in bash commands, names appearing in angle-brackets should be replaced with your choice of appropriate name according to the semantics.

`django-admin -h` is the command for help which you can avail on your terminal.

{%highlight bash%}
django-admin startproject <project-name>
django-admin startapp <app-name>
{%endhighlight%}
These commands are used to create a project. And inside a project, second command is used to create an app.
When a project is created you find manage.py inside the project folder.

{%highlight bash linenos%}
python manage.py runserver <ip-address>:<port>
python manage.py syncdb
#make changes
python manage.py makemigrations
python manage.py migrate
{%endhighlight%}
These commands are used to run a server at a given ipaddress and port(if left blank, shall run at http://localhost:8000/). `syncdb` option is used to sync the database with creation of tables if ran for the first time will ask for creation of superuser and changes or insertion of data when run in future. Migrations django help us to change the structure of tables as we change the models during development. `makemigrations` is used to find migrations and apply them.

After the server has been started, visit your [admin panel](http://localhost:8000/admin/) at http://localhost:8000/admin/. The username and password are the ones you provided during superuser creation. After logging in you shall find Users and UserGroups in your dashboard under Authentication and Authorisation app which are provided default by django. Inorder to have a graceful and bootstrap look to the admin panel one can install `grappelli` app using pip. 

{%highlight bash%}
pip install django-grappelli
{%endhighlight%}
After this is installed, you must add the app `grappelli` to the tuple of `INSTALLED_APPS` in your project settings.py file. Also, you need to add the following to your urls.py file in project folder.
Your urlpatterns inside urls.py file should look similar to this or atleast start this way inorder to take leverage of the django-grappelli.
{%highlight python linenos%}
urlpatterns = patterns('',
    # Examples:
    # url(r'^$', 'exapmpleproject.views.home', name='home'),
    # url(r'^appname/', include('app.urls')),

    url(r'^admin/', include(admin.site.urls)),
    url(r'^grappelli/', include('grappelli.urls')),
    #Other urls
    #end url() with a , since these are tuple entries
    )
{%endhighlight%}

Now visit the admin panel, and you shall find a cool interface.

Inorder to change the default Grappelli appearing on the admin panel, add the following to your settings.py file anywhere
{%highlight python%}
GRAPPELLI_ADMIN_TITLE="<project-name>"
{%endhighlight%}

Now, we shall try to create a page at the `base-url` that is `http://localhost:8000/`. Inorder to do this, we should first create an app using `django-admin startapp <app-name>` command inside the folder which contains the `manage.py` file. Let's give the app-name as 'myapp'. Add this app to the tuple of `INSTALLED_APPS` in settings.py by entering the app name in single quotes at the last of existing entries terminating with a comma','. Your INSTALLED_APPS tuple should similar to the following.
{%highlight python linenos%}
INSTALLED_APPS = (
    'grappelli',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'myapp',
)
{%endhighlight%} 
`django.contrib.admin` and `django.contrib.auth` provide us admin panel and custom built-in authentication.

Now, open views.py file inside the `myapp` folder with your favourite editor. You will have some imports by default in it done for you by django. Views are created as methods and then urlpatterns are defined by using these methods. So, create a function named `index` and return a template with request using render. Your views.py shall look similar to this.
{%highlight python linenos%}
from django.shortcuts import render
# Create your views here.
def index(request):
	return render(request,'myapp/index.html')
{%endhighlight%}

Now we need to create a folder named `templates` in project-root directory i.e the directory containing manage.py file. We need to update settings.py as shown to make it understand where the templates are stored. Add exactly the following to the ending of settings.py file. Also, create a folder named `static` in project-root directory. Inside `static` folder create folders named `css`,`js` and `images`.
{%highlight python%}
TEMPLATE_DIRS = ('./templates',)
{%endhighlight%}
Now copy [bootstrap.min.css](http://maxcdn.bootstrapcdn.com/bootstrap/3.3.1/css/bootstrap.min.css) into `static/css` and jquery.min.js and [bootstrap.min.js](http://maxcdn.bootstrapcdn.com/bootstrap/3.3.1/js/bootstrap.min.js) into `static/js` folders.

Now inside templates folder create a folder named `myapp` and create a file named `index.html` inside `myapp` folder. Also create a folder named `layout` inside templates folder. Create a file named `header.html` inside `layout` folder. The header.html file should be as follows:
{%highlight html+django %}
{%raw%}
{% load staticfiles %}
<!DOCTYPE html>
<html lang="en">
<head>
	<title> {{title}}</title>
	<link rel="stylesheet" type="text/css" href="{% static "css/bootstrap.min.css" %}">
	<script type="text/javascript" src="{% static "js/jquery.min.js" %}"></script>
	<script type="text/javascript" src="{% static "js/bootstrap.min.js" %}"></script>
</head>
<body>
<div class="navbar navbar-default">
  <div class="navbar-header">
    <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-responsive-collapse">
      <span class="icon-bar"></span>
      <span class="icon-bar"></span>
      <span class="icon-bar"></span>
    </button>
    <a class="navbar-brand" href="#">Project-Name</a>
  </div>
  <div class="navbar-collapse collapse navbar-responsive-collapse">
    <ul class="nav navbar-nav">
      <li class="active"><a href="#">Active</a></li>
      <li><a href="#">Link</a></li>
      <li class="dropdown">
        <a href="#" class="dropdown-toggle" data-toggle="dropdown">Dropdown <b class="caret"></b></a>
        <ul class="dropdown-menu">
          <li><a href="#">Action</a></li>
          <li><a href="#">Another action</a></li>
          <li><a href="#">Something else here</a></li>
          <li class="divider"></li>
          <li class="dropdown-header">Dropdown header</li>
          <li><a href="#">Separated link</a></li>
          <li><a href="#">One more separated link</a></li>
        </ul>
      </li>
    </ul>
    <ul class="nav navbar-nav navbar-right">
      {% if not user.is_authenticated%}
      <li><a href="/login">Login</a></li>
      <li><a href="/signup">Signup</a></li>
      {% elif user.is_authenticated %}
      <li class="dropdown">
        <a href="#" class="dropdown-toggle" data-toggle="dropdown">Dropdown <b class="caret"></b></a>
        <ul class="dropdown-menu">
          <li><a href="#">Action</a></li>
          <li><a href="#">Another action</a></li>
          <li><a href="#">Something else here</a></li>
          <li class="divider"></li>
          <li><a href="#">Separated link</a></li>
        </ul>
      </li>
      <li><a href="/logout">Logout</a></li>
      {% endif %}
    </ul>
  </div>
</div>
<div class="content-block">
{% block content %}{% endblock %}
</div>
</body>
</html>
{%endraw%}
{%endhighlight%}
This is a layout with dummy nav-bar. We should change the links accordingly.`loadstatic` tag on top will provide us with static links. The `static` filter tag is used to generate static folder prefixes in urls.
The `block` tag is used to insert the content of other pages which extends this header.html page.

Now edit the `index.html` file inside `myapp` folder as follows
{% highlight html+django %}
{% raw %}
{% extends "layout/header.html" %}
{%block content%}
<div class="container">
	<div class="jumbotron">
		<h1>Welcome to my <Project-Name></h1>
	</div>
</div>
{% endblock %}
{% endraw %}
{% endhighlight %}
Now we need to update urlpatterns in urls.py with our method in views.py as follows
{% highlight python linenos %}
from django.conf.urls import patterns, include, url
from django.contrib import admin

urlpatterns = patterns('',
    url(r'^admin/', include(admin.site.urls)),
    url(r'^grappelli/', include('grappelli.urls')),
    url(r'^$','myapp.views.index'),
)

from django.conf import settings
if settings.DEBUG:
    urlpatterns += patterns('',
        url(r'^static/(?P<path>.*)$', 'django.views.static.serve', {
            'document_root': settings.STATIC_ROOT,
        }),
)

{%endhighlight %}
The last urlpattern contains `$` which means the site shall point to the root i.e `/`. If you want to create a url say `localhost:8000/myurl` then add `url(r'^myurl/','myapp.views.methodToMyurl')` to urlpatterns.

Run the server and head to the base-url i.e [here](http://localhost:8000/). You should find that your awesome page has been created.

Explore more by creating new views, templates and updating the urlpatterns.

More on models and creating login forms shall be written in detail in upcoming posts.

That's all for today, the next post shall be about jekyll blogs. :blush: