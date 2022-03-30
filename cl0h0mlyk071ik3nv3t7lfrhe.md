## Tips to Become Smarter at Django

Django is a popular back-end framework. A lot of developers and high-ranked companies are using it, but what is the magic word? Can you guarantee your next move?!

### Model Before Starting
How do you build a structure without even at least imagining it in your mind? That's why great people always have a piece of paper in their pockets. There is a quote from __J.K. Rowling__ that says:

>Understanding is the first step to acceptance, and only with acceptance can there be recovery.

So what does that mean in the tech world? Modeling your tables allows you to figure out the next steps throughout your project development. Imagine you have tons of views and forms. In the template development, you understand that there is something missing from the `Student` table. That could be super cool if I store the student's emails on the table.

After this implementation, you are now in really big trouble. You should cut down the template development in order to start mailing configurations, what's more, you need to set up a verification system to verify those email addresses. You're stuck and your stepbro is sleeping. I know. What's the solution at this moment? Backing into `$ python manage.py startapp myapp` for sure.

The best practice is to prevent making these mistakes in your projects and that's why I suggest you design your database before you head into the commands and codes.

### Hard-coded URLs; Run Away
You've already passed the [Poll project from the official Django website](https://docs.djangoproject.com/en/4.0/intro/tutorial01/) and trying to create your first weblog. Designing your navbar for a better UI by the way. Your sun is still shining until you decide to change the `/about` endpoint to `/aboutme`. You run into problems that are not quite weird, to be honest. You've been using the hard-coded URLs.

```python
from django.urls import path

from . import views

urlpatterns = [
    # ...
    path('/aboutme', views.about, name='about'),
    # ...
]
```

```html
<nav>
    <ul>
        <li><a href="/about">About Me</a></li>
    </ul>
<nav>
```

You might have figured out the issue. The problem is occurring because of that `href` URL. You quickly change it to `/aboutme`. Did you fix it entirely? What if you had to change all your endpoints? Are you going to change the `href` URLs from each anchor (`</a>`)?

```html
<nav>
    <ul>
        <li><a href="{%url 'about' [params]%}">About Me</a></li>
    </ul>
<nav>
```

From now on. whenever you change the app URL, the `href` address will be changed based on your endpoint in `yourapp/urls.py`.

### QuerySet Optimizations
Select only those fields you need to show in your templates. (You actually put them in a dictionary variable called `context`). Imagine you want to show all book cover images in a template. You kept up with the following function view.

```python
def show_covers(request):
    books = Book.objects.all()
    return render(request. 'app/covers.html', {'books': books})
```

Your template will have a really long junky path to do it for you when you have millions of books in your database. You just need `book.cover` data, so that you better prevent waiting for the entire book records from the database engine. Use `values()` to optimize your requests in this case.

```python
def show_covers(request):
    covers = Book.objects.values('cover')
    return render(request. 'app/covers.html', {'covers': covers})
```

Nice queryset optimization yea? I'm into it. It takes less time to get the result than using the `all()` method though.

### Use `message` Module
In some cases, you may need to report some actions done by the end-user. The `message` module is a Django built-in module that allows you to report them all whether they were successful or not to the end-user after each page reload. This module is explained in action in my [Email Subscriber](https://github.com/lnxpy/emailsubscriber) project.

For more information about this module, check out the [official documentation](https://docs.djangoproject.com/en/3.2/ref/contrib/messages/).

### Use `shell` and Tests
Django has a lot of facilities and tools in order to be able to design our projects with less complexity, pain, and nervousness as a developer. Django shell is one of them. This tool allows you to create small snippets to find out whether they are working. As a Django developer, I use this tool whenever I stuck in my project tasks. Be careful about what you do in your shell. In most cases, you use shells in order to interact with ORM and the database. All you do will affect the database by default. That's why I recommend you to use tests to clarify your querysets, authentications, and all SQL operations. Django Test creates a new in-memory database that has the same table structures as your real tables have. After each execution, the cached databases will be destroyed.

#### Shared Cache Technology
Basically, the SQL databases have a feature called **Shared Cache** which is about the ability to create a cached in-memory database that is completely separated from the main database. All connections will be separated too. Django Test creates the connections between its core and the Shared Cache connections. Those connections (based on the configurations) will be lost and the Shared tables will be removed.

### Have a Localized Settings
When you have a localized version of your project, you won't be able to run the server locally with the settings that have been configured for the deployment server like the security configurations as a case.

```python
# Security Zone
CSRF_COOKIE_SECURE = True
SESSION_COOKIE_SECURE = True

SECURE_BROWSER_XSS_FILTER = True
SECURE_CONTENT_TYPE_NOSNIFF = True

SECURE_SSL_REDIRECT = True

SECURE_HSTS_SECONDS = 86400  # 1 day
SECURE_HSTS_INCLUDE_SUBDOMAINS = True
SECURE_HSTS_PRELOAD = True
```

What you need is to create a file named `local_settings.py` right next to `settings.py` and override the settings that are critical in the local environment like disabling the `# Security Zone`, setting the debug mode on by `DEBUG=True`, and so on. Finally, you should override all those variables in your main settings file. (make sure you put the following snippet at the end of the `project/settings.py` file)

```python
# ...
try:
    from .local_settings import *
except:
    pass
```

The `local_settings.py` file is being ignored by some version control systems such as Git.
 
### Don't Think About The Front-end
You are responsible for creating a strong and optimized back-end service. Creating those templates is not why you are hopping into your favorite editor. Nothing is perfect. After millions of commits, your code is still optimizable.

### Keep Learning
And last but not least, keep learning new things. They allow you to solve your problems by spectating your project from others' points of view.