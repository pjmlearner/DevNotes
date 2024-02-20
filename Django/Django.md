# Django

## What is Django

* a high-level Python base web-framework
* it is a backend/server-side framework
* Follows the Model-View-Template (MVT) design pattern
* ![image-20240208161228558](C:\Git\Github\DevNotes\Django\image-20240208161228558.png)



## What is PIP

* Pip is a tool that used to install and manage Python packages

* Python packages are available at https://pypi.org

* Command to install a package

  ```
  pip install <package name>
  ```



## What is a Virtual Environment

* a virtual environment is a tool to isolate our independent projects with its own unique set of dependencies

* Commands:

  *  to install virtual environment package

  ```
  pip install virtualenv
  ```

  * create a virtual environment

  ```
  virtualev <name-virtual-env-folder>
  ```

  * activate virtual environment

  ```
  <name-virtual-env-folder>\Scripts\activate
  ```

  * deactivate virtual environment

  ```
  <name-virtual-env-folder>\Scripts\deactivate
  ```

* *Ensure you're in an activated virtual environment when installing packages for your project, otherwise they'll be installed globally*



##  Create a Django Project

### Install Django

* within the virtual environment run:

```
pip install django
```

### Create Django Project

```
django-admin startproject <projectname>
```

### Run server

* confirm Django Project is installed and working

* in command prompt ensure you're within the project folder (CD into it) then run:

  ```
  python manage.pg runserver
  ```

* the response from the command will contain an IP address for the server, which you can then go from your web browser



## Django Default Files

* db.sqlite3
  * The first time the python server is run, this default database is created by Django
  * This can be changed by settings.py file
* manage.py
  * used to run administrative tasks
* _init_.py
  * blank file
  * purpose is to treat directories that are added to it as modules
* asgi.py
  * asynchronous server gateway interface
  * allows for asynchronous development
* settings.py
  * list installed apps
  * setup templates
  * setup static files (CSS, JavaScript, Images)
  * setup database
  * setup middleware
    * security, csrf, etc
  * authorization password validations
* urls.py
  * setup URLs
* wsgi.py
  * web server gateway interface
  * primary role is forwarding a request from a web server (e.g. APACHE) to Django



# Django App

## The Concept of a Django App

### What is a Django App?

A Django Project:

* is composed of a collection of various settings, configurations, apps
* we an either have one or multiple apps in a single django project

A Django App:

* an application that serves a unique purpose
* an app typically consists of URLs, views, templates and models



## Configure a Django App

### Create a Django App

* command to create a django app:

```
django-admin startapp <name-of-app>
```

### Install App in Project

* go settings.py > find the INSTALLED_APPS section and add the name of your app

* Example

* ```python
  INSTALLED_APPS = [
      'django.contrib.admin',
      'django.contrib.auth',
      'django.contrib.contenttypes',
      'django.contrib.sessions',
      'django.contrib.messages',
      'django.contrib.staticfiles',
      '<name-of-app>',
  ]
  
  ```

### Migrate Default Installed Apps

* when you run the server you may notice a response:

  * *You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.*
  * the above message is notifying you that the default installed Django apps have not been applied to your project to do so we use `migrate`

* migrate the default installed apps

  * what this will do is create the corresponding database tables to the models that are found in the default django installed apps
    * i.e. running a migration on django.contrib.auth will create the database entites associated to the auth app such as a users table
  * command to run the migration

  ```
  python manage.py migrate
  ```

### Django App Default Files

* admin.py
  * configuration file for our Django admin page
* models.py
  * models => database tables
* views.py
  * setup business logic in handling our http requests and responses
* apps.py
  * informational file
* tests.py
  * for unit testing



# URLs, Views, Templates

## What are URLs and Views?

* URL

  * A Uniform Resource Locator (URL) is used to locate a particular web page on your browser

  ![image-20240216152214516](C:\Git\Github\DevNotes\Django\image-20240216152214516.png)

* Views
  * Views are Python functions or classes that are used to return a response.
  * ![image-20240216153443350](C:\Git\Github\DevNotes\Django\image-20240216153443350.png)
  * In Django, a view is responsible for processing an incoming HTTP request and returning an HTTP response. Views encapsulate the application logic for a specific URL route. They can be implemented as functions (function-based views) or classes (class-based views). Django views correspond closely to the concept of controllers in other frameworks like ASP.NET MVC.
* Best Practice
  
  * create a urls.py file on the app level (in your app folder) and use this for your app urls, instead of using the default urls.py file within the entire project

##  A Simple Web Page

* an example of setting up the project and app URLs and Views to serve a web page

### urls.py

#### project

```python
from django.contrib import admin
from django.urls import path, include  #the include function is imported

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('crm.urls')),  #'' denotes we're attaching to the hostname path, and include('crm.urls') is the include function that identifies the app 'crm' (from app's app.py file) and the app's urls.py file
]
```



#### app

```python
from django.urls import path
from . import views  #import the views.py file within the app path

urlpatterns = [
    path('register', views.register), #displays content from the views.py file's register function, and ties that to the url path of 'http://127.0.0.1:8000/register'
    path('', views.home), #displays content from the views.py file's home function, and ties that to the url path of 'http://127.0.0.1:8000/'
]
```



### views.py

#### app

```python
from django.shortcuts import render
from django.http import HttpResponse

def home(request):
    return HttpResponse('This is home.')

def register(request):
    return HttpResponse('This is a registration page!')
```



## Template

a template is a text file that represents the layout and structure of a particular file that is marked-up using the Django Template Language (DTL)

### Configure Template Rendering

#### best practice

* create a template folder within your Django app, and within the template folder create another folder with the same name as your Django app, this is to ensure we don't have any namespace issues

* example

  * django-app
    * templates
      * django-app-name

  ![image-20240218143904578](C:\Git\Github\DevNotes\Django\image-20240218143904578.png)

  

#### template html pages

* create html files within the templates/<django-app-name> folder

  ![image-20240218145646530](C:\Git\Github\DevNotes\Django\image-20240218145646530.png)

* index. html

  ```html
  <html>
  <h1>This the home page.</h1>
  <p>Welcome to my website!</p>
  </html>
  ```

* register.html

  ```html
  <html>
  <h1>
      This the register page.
  </h1>
  </html>
  ```

* modify views.py file

  ```python
  from django.shortcuts import render
  from django.http import HttpResponse
  
  def home(request):
      return render(request, 'crm/index.html') #use render function to serve the specified template html file.  django can auto-resolve the template folder, but the app-name (crm).
  
  def register(request):
      return render(request, 'crm/register.html')
  ```

  

### Template Inheritance

* allows you to build a base template (parent or 'skeleton' template), which contains elements that you can reuse in other templates
* it defines a set of blocks that child templates can override from the base template
* The Django Template Language (DTL) provides a set of built-in tags that can help you to carry out template inheritance

#### What is an element?

* an element can be defined as a component that we can re-use
  * buttons
  * search bar
  * navigation bar
  * form

#### Configure Template Inheritance 

* example

  * we add a parent template to our template/<app-name> folder

  ```html
  <!-- parent template is called base.html  -->
  <html>
      <h1> Website underdevelopment</h1>
      <hr>
      <!-- Blocks are used as placeholders for child templates to replace or extend the section -->
      {% block content %}
  
          <p> This is the parent block.</p>
      
      {% endblock %}
  </html>
  ```

  * our child templates inherit from the parent template

  ```html
  {% extends 'crm/base.html' %} <!-- django tag to inherit from parent template -->
  
  <!-- all html within the block will replace the parent block it inherits from-->
  <html>
  {% block content %}
      <h1>This the home page.</h1>
      <p>Welcome to my website!</p>
  {% endblock %}
  
  </html>
  ```

  ![image-20240219012740891](C:\Git\Github\DevNotes\Django\image-20240219012740891.png)



## Django Template Language (DTL)

* is a so-called "mini-language" that allows us to write logic within our templates
* we can use it for:
  * pass variables to our templates (we use {{}} to pass variables)
  * create it statements to handle our conditions
  * create for loops to loop through our data 
* list and dictionaries
  * each dictionary is almost 'object-like'

```python
clientList = [
    {
        'id' : '1',
        'name' : 'John Doe',
        'profession' : 'Electrical engineer'
    },
]
```

 ![image-20240219231701442](C:\Git\Github\DevNotes\Django\image-20240219231701442.png)



### Passing Variables to Our Template

* views.py

  ```python
  def home(request):
      context = {'first_name' : 'John', 'last_name' : 'Doe'} #create a dictionary assigned to context variable
      return render(request, 'crm/index.html', context) #pass the dictionary variable as the third parameter
  ```

  

* index.html

  ```html
  {% extends 'crm/base.html' %}
  
  <html>
  {% block content %}
      <h1>This the home page.</h1>
      <p>Welcome to my website!</p>
      <h5>Hello my name is {{first_name}} {{last_name}}</h5>  <!-- use DTL to display the values in the web page -->
  {% endblock %}
  
  </html>
  ```

  

### Built-In Tags

* DTL comes along with built-in tags
* they are defined as {% %} and allows us to write python-styled logic
* Examples
  * {% csrf_token %} - needed in a template when working with a database
  * {% extends %} - needed for template inheritance
  * {% if %} ... {% end if %}
  * {% for %} ... {% endfor %}