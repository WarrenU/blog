---
title:  "Django Shell Plus Imports"
date:   2017-01-25 20:19:42 -0800
---

The topic of this blog is about controlling import order resolution when using the django extension, shell_plus:
[http://django-extensions.readthedocs.io/en/latest/shell_plus.html](http://django-extensions.readthedocs.io/en/latest/shell_plus.html )

Shell plus is an interactive python shell that will load in your apps DB models:

{{< highlight html >}}
django python manage.py shell_plus
{{< /highlight >}}

When you do this, by default, all of your app's models will be imported.
But, there is a way you can control which models get imported, and the order in which they do.
For example: If you want to preimport a model/module before the shell plus imports,
you should add the following to your configuration file in your django project:

{{< highlight html >}}
SHELL_PLUS_PRE_IMPORTS = (
    ('project.app.models', 'Car')
)
{{< /highlight >}}

To import after the shell plus imports you simply change the variable to SHELL_PLUS_POST_IMPORTS:
{{< highlight html >}}
SHELL_PLUS_POST_IMPORTS = (
    ('project.app.models', 'Person')
)
{{< /highlight >}}

This is helpful if you have a dependency or conflicting namespace (uh-oh! ideally you wouldn't).

You can also configure shell_plus to not import parts of your app:
Let's say we have an app called: Vehicles, which contains 2 model classes: "Car" and "Boat".
You can configure shell plus to not load "Car" for example:
{{< highlight html >}}
SHELL_PLUS_DONT_LOAD = ['vehicles.Car']
{{< /highlight >}}
In the above example, the Vehicles.Car model will not be imported, but other Models from the Vehicles app will (Boat).
You can provide mutliples to this configuration, and even include a whole app, let's say a 'documents' app:
{{< highlight html >}}
SHELL_PLUS_DONT_LOAD = ['documents', 'vehicles.Car']
{{< /highlight >}}
