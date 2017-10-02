---
title:  "Django Shell Plus Imports"
date:   2017-01-25 20:19:42 -0800
draft: true
---

Welcome to my first blog post!

When using django's shell plus command:

{% highlight ruby %}
django python manage.py shell_plus
{% endhighlight %}

You will get your application's database models pre-imported into an interactive python shell.
If you haven't used it before it is really handy and nifty for hackin'.

But have you ever wanted to change the order in which the shell imports these apps/models?
You Can.

For example: If you want to preimport a model before the shell plus imports you could do:

{% highlight ruby %}
SHELL_PLUS_PRE_IMPORTS = (
    ('project.app.models', 'Car')
)
{% endhighlight %}

To import after the shell plus imports you simply change the variable to SHELL_PLUS_POST_IMPORTS:
{% highlight ruby %}
SHELL_PLUS_POST_IMPORTS = (
    ('project.app.models', 'Person')
)
{% endhighlight %}

This is helpful if you have a model name that conflicts with an app that is imported from Shell Plus.

You can also command it to skip imports entirely:
You pass it a list of apps and or a model from an app as so:
{% highlight ruby %}
SHELL_PLUS_DONT_LOAD = ['app', 'app1.Car']
{% endhighlight %}

So the above is ignoring app's imports entirely and from app1 will not import model1.

More on shell plus can be found @ the documentation
[http://django-extensions.readthedocs.io/en/latest/shell_plus.html](http://django-extensions.readthedocs.io/en/latest/shell_plus.html )
