---
layout: post
title: "Serving Static Files in Django"
date: 2014-12-26 12:00
authors: [dakota]
description: Getting started serving static files in Django, especially for development, is a confusing mess. However, it doesn't have to be so hard - you can serve all the static files you need after only four simple steps.
tags: [programming, django, web, tutorial]
---

Getting started serving static files in Django, especially for development, is a confusing mess. While it makes sense that you should use a full-fledged server like Apache or Nginx for production, setting up a development environment and getting it working with Django is much harder and more confusing than it should be.

However, thanks to the magic of Python, getting off the ground and running can be incredibly easy. For development purposes, it's just four steps.

This article assumes you already have a Django 1.7 project set up in a \*nix system, and uses python 3 - but it should be easily adaptable to other python or Django versions.

### Step One: Create a Static Directory
The first step is to  create a directory to hold all of your static files (this is *not* using Django's automatic static-collection functionality). I generally create it at the top level of the Django project, but it's entirely up to you. Feel free to make as many subdirectories as you need.

### Step Two: Create a Symlink
However, Django has static files of its own. In order to serve Django's static files as well as yours, we will create a symlink pointing to Django's static file location. This location has two parts; Django's path, and the path to the static files within Django.

The path to Django itself can be found by opening python, importing Django, and running `django.__file__`. Note that `__init__.py` is not part of the path. The location of the static files within Django, for Django 1.7, is `contrib/admin/static/admin`. To get the full path, simply concatenate the two (minus `__init__.py`, of course).

When I run `django.__file__` on my machine, I get `/home/dnelson/.pyenv/versions/3.3.3/lib/python3.3/site-packages/django/__init__.py`. This means that the full path to Django's static files on my system is `/home/dnelson/.pyenv/versions/3.3.3/lib/python3.3/site-packages/django/contrib/admin/static/admin`.

Once you've found where Django keeps its static files, create a symlink from your static files directory to Django's. This is done by changing to your static directory and executing `ln -s /path/to/django/static/files ./admin`. You can see what this looks like on my system in the screenshot below.

{:.center}
![command to issue in order to start a static server for use with Django]({{site.url}}/assets/django-static-symlink.png){: .image }

### Step Three: Configure Django

Inside Django's `settings.py`, change the value of `STATIC_URL` to `http://localhost:8001/`. Substitute whatever port you want for 8001, and note that the trailing slash is critically important.

### Step Four: Start the Static Server!
Now that you have your static directory set up, cd to it, and run `python -m http.server 8001`. (If you used a different port in configuring Django in step three, use that port instead of 8001.)

### That's it!
Congratulations, you're done! To recap, you:

  + Created a folder in which to put all of your static files,
  + created a symlink so that Django's static files will be served alongside your own,
  + configured Django to fetch static files from your server, and
  + started serving the static files for Django to use.

In order to use these static files in your Django templates, put {% raw %}`{% load staticfiles %}`{% endraw %} near the front of each of your templates (even if they're inherited), then refer to static files as {% raw %}`{% static filename.png %}`{% endraw %}. For example, if you have a javascript file at `staticdir/js/awesome.js`, you'd load it as {% raw %}`{% static js/awesome.js %} `{% endraw %}.

If this tutorial worked well for you - or didn't - make sure to leave a comment saying so. Thanks, and happy hacking!
