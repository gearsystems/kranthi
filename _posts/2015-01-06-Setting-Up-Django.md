---
layout: post
title: Setting Up Django
comments: True
redirect_from: "/2015/01/05/Setting-Up-Django/"
permalink: setting-up-django
---

##Hands on with Django

As said in my earlier post, things about django shall be written soon. This post shall carry some insight into the `Django framework` from my perspective. I shall provide the details of setting up of django framework in this post and making a small login form and registration form in the coming tutorials.

As for any project, requirements are as important as delivering a product. Without requirements, its obviously difficult to start working or build something. So, below are the requirements for django:

<table>
	<thead>
		<tr>
			<th>Name of requirement</th>
		</tr>
	</thead>
	<tbody style="text-align:center;">
		<tr>
			<td>python-dev</td>
		</tr>
		<tr>
			<td>libmysqlclient-dev</td>
		</tr>
		<tr>
			<td>pip</td>
		</tr>
		<tr>
			<td>virtualenv</td>
		</tr>
		<tr>
			<td>Django</td>
		</tr>
		<tr>
			<td>MySQL-python</td>
		</tr>
	</tbody>
</table>

##Installing the requirements
The above mentioned requirements are easy or moderately easy to setup. I shall provide you with the commands to install them on a Linux machine.(I am running a ubuntu 14.04 machine)

If you donot have MySQL installed in your machine, you can install it using the following commands:
{% highlight bash %}
$ sudo apt-get install mysql-server
$ sudo apt-get install mysql-client
{% endhighlight %}
You will be asked for username and password during installation. After installation, try out mysql using this command:
{%highlight bash%}
mysql -u<username> -p<password>
{%endhighlight%}
Replace `<username>` and `<password>` with your username and password provided during installation.

We need `python-dev` and `libmysqlclient-dev` for the `MySQL-python` module to install correctly from the pip. PIP is Python Packaging Index which serves alike aptitude to provide required modules or libraries. The command below installs python-dev and libmysqlclient-dev on ubuntu:

{%highlight bash%}
sudo apt-get install build-essential python-dev libmysqlclient-dev
{%endhighlight%}
For Windows users, download Active state python and also setup [cygwin](http://cygwin.com) so that you have a bash. Commands like source, wget etc are not available in windows command prompt. Hence, we need cygwin bash for linux experience. You can use mysql from the lampp/xampp stack too instead of setting it up the command line way.

Now, you should have python with version 2.6 or 2.7+ . Do not download Python 3+ since I am going to explain/write my tutorials in python 2.7+

To install pip, in ubuntu you can use the following command:
{% highlight bash %}
apt-get install python-pip
{% endhighlight %}
Windows users can download the [get-pip.py](https://bootstrap.pypa.io/get-pip.py) file and run the following command:
{% highlight bash %}
python get-pip.py install
{% endhighlight %}
Now, you should have pip installed. You can check it by typing `pip -V` in the terminal to view the version.

Using pip, we shall procure virtualenv, django , mysql-python and grappelli.

###Installing virtualenv
Virtualenv is used to create virtual environment so that development can be done irrespective of environment. One might work in Ubuntu(linux) and other on windows. Using virtualenv, one can bridge the gap. virtualenv provides us with bunch of requirements used specific to the project and also use specific version of library in a particular project.This way, we can use different versions of libraries in various projects with least hurdles. To install virtualenv,use:
{% highlight bash %}
pip install virtualenv
{% endhighlight %}
You can create a virtualenv by using the following command:
{% highlight bash %}
virtualenv venv
{% endhighlight %}
In linux, this shall create a folder with venv containing python executables inside it. We can activate the virtualenv by executing the activate file inside bin folder using source command as
{% highlight bash %}
source venv/bin/activate
{% endhighlight %}
Windows users should use the following command in the cygwin bash:
{% highlight bash %}
source venv/Scripts/activate
{% endhighlight %}
Type `deactivate` to come out of the virtual environment anytime.

###Installing Django
Now, we can install Django happily. Before installing it, we should activate the virtualenv we created. Otherwise, the package we install using pip shall enter into global package list in our machine. We wouldn't want that. We need Django only in the virtualenv we created. We shall download Django using pip.
{% highlight bash %}
pip install Django
{% endhighlight %}
This command shall install Django.That's it.

###Installing MySQL-Python
We need MySQL-Python for Django to make use of mysql databases. MySQL-Python shall provide us with connectors and cursors to query the mysql databases. It acts as a bridge between mysql and python. To install it:
{% highlight bash %}
pip install MySQL-Python
{% endhighlight %}
Comment if you have any problems installing the package.

###Creating our first django project
{% highlight bash %}
django-admin startproject MyAwesomeProject
{% endhighlight %}
The above command shall create a project folder named MyAwesomeProject with manage.py and MyAwesomeProject folder inside it. manage.py is heart of django project.
cd(change directory) to your project folder.
{% highlight bash %}
django-admin startapp myapp
{% endhighlight %}
This command shall create an app with name myapp. Inorder to use this app, we should include it in the INSTALLED_APPS  in settings.py present in MyAwesomeProject folder. Add 'myapp' to the last of existing tuple and end it with ',' before closing the ')'

Also, if we are using mysql database, instead of the default text based sqlite database, we need to modify the DATABASES dictionary in settings.py as:
{%highlight python%}
DATABASES = {
	'default': {
	'ENGINE'  : 'django.db.backends.mysql',
	'NAME'    : '',#database name here
	'USER'    : '',#your username
	'PASSWORD': '',#your password
	'HOST'    : 'localhost',
	'PORT'    : '3036',
	}
}
{%endhighlight%}

Now, open the terminal and type the following command to run the server:
{%highlight bash%}
python manage.py runserver
{%endhighlight%}
You should be able to see that server is up and running at `127.0.0.1:8000`. Open your browser and type in the same address i.e [http://127.0.0.1:8000](http://127.0.0.1:8000). You will find a page saying it works.

To stop the server, press `ctrl`+`c`
:v:
Hurray! We have successfully setup a django server and seen it working. We also have setup mysql and mysql-python.
:smile:

The next post shall introduce you some basic Object Relational Mapping and how to create a login form and registration form. Feel free to comment or discuss any problems you face. I shall reply when I get notified.:sunglasses: