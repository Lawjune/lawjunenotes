# Part 1

## 1.1 Get Started

### 1.1.1 Introduction

**Learn to build production-grade backends**

**Build an e-commerce application with Django**

### 1.1.2 Prerequisites

**Python
* basics
* classes
* inheritance
**

**Relational Databases
* tables
* columns
* keys
* relationships
**

### 1.1.3 How to Take this Course

## 1.2 Django Fundamentals

### 1.2.1 Introduction

**IN THIS SECTION
* Introduction to Django
* Fundamentals of web development
* Setting up the development environment
* Your first Django project
* 2 essential debugging techniques
**

### 1.2.2 What is Django

**Free and open-source framework for building web apps with Python**

**DJANGO FEATURES
* The admin site
* Object-relational mapper (ORM)
* Authentication
* Caching
**

**Ferrai vs Trucks => Performance isn't everything
* Maturity
* Difficulty
* Stability 
* Community
**

*Django comes with a LOT of features... 
*But you don't have to use them all*


### 1.2.3 How the Web Works

### 1.2.4 Setting Up the Development Environment

```sh
python --version
`=>
Python 2.7.16
```

```sh
python3 --version
`=>
Python 3.10.0
```

```sh
pip3 install pipenv
```

*Install `python` extension on vscode*

### 1.2.5 Creating Your First Django Project

```sh
cd Desktop 
mkdir storefront
cd storefront
pipenv install django
`=>
✔ Successfully created virtual environment! 
Virtualenv location: /Users/mac/.local/share/virtualenvs/storefront-O0ZRZ9iG
Creating a Pipfile for this project...
Installing django...
...
...
...
```

```sh
pipenv shell
`=>
Launching subshell in virtual environment...
 . /Users/mac/.local/share/virtualenvs/storefront-O0ZRZ9iG/bin/activate
mac@madeMacBook-Pro storefront %  . /Users/mac/.local/share/virtualenvs/storefront-O0ZRZ9iG/bin/activate
```

```sh
django-admin
`=>
Type 'django-admin help <subcommand>' for help on a specific subcommand.

Available subcommands:

[django]
    check
    compilemessages
    createcachetable
    dbshell
    diffsettings
    dumpdata
    flush
    inspectdb
    loaddata
    makemessages
    makemigrations
    migrate
    runserver
    sendtestemail
    shell
    showmigrations
    sqlflush
    sqlmigrate
    sqlsequencereset
    squashmigrations
    startapp
    startproject
    test
    testserver
```

```sh
django-admin startproject storefront .
```

```sh
python manage.py runserver
```

### 1.2.6 Using the Integrated Terminal in VSCode

```sh
pipenv --venv
`=>
/Users/mac/.local/share/virtualenvs/storefront-O0ZRZ9iG
```

*Input `/Users/mac/.local/share/virtualenvs/storefront-O0ZRZ9iG/bin/python` into the `Select python interpreter` of vscode.*

***/.vscode/settings.json***
```json
{
  "python.pythonPath": "/Users/mac/.local/share/virtualenvs/storefront-O0ZRZ9iG/bin/python"
}
```

### 1.2.7 Creating Your First App

```sh
python manage.py startapp playground
```

*Register in /storefront/settings.py*

```pythons
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    # 'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'playgroud'
]
```

### 1.2.8 Writing Views

*/playground/views.py*
```python
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.
# Reuest -> Response
# Request handler
# action

def say_hello(request):
    # Pull data from db
    # Transform
    # Send email
    return HttpResponse("Hello World!")
```

### 1.2.9 Mapping URLs to Views

*Create `urls.py` inside playground folder*
*/playground/urls.py*
```python
from django.urls import path
from . import views

# URLConf
urlpatterns = [
    path('/playground/hello/', views.say_hello)
]
```

*Go to /storefront/urls.py*
```python
from django.contrib import admin
from django.urls import path
from django.urls.conf import include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('playground/', include('playground.urls'))
]
```

=>


*/playground/urls.py*
```python
from django.urls import path
from . import views
```

# URLConf
urlpatterns = [
    path('hello/', views.say_hello)
]
```

### 1.2.10 Using Templates

*Create `templates` folder under `playground`*
*Add `hello.html` under `templates` folder`*

```html
{% if name %}
<h1>Hello {{name}}</h1>
{% else %}
<h1>Hello World</h1>
{% endif %}
```

*/playground/view.py*
```python
def say_hello(request):
    return render(request, 'hello.html', {'name': 'Lawjune'})
```

### 1.2.11 Debugging Django Applications in VSCode

### 1.2.12 Using Django Debug Toolbar

**Inside the virtual environment**
```sh
pipenv install django-debug-toolbar
```

https://django-debug-toolbar.readthedocs.io/en/latest/installation.html#prerequisites

## 1.3 Building a Data Mode

### 1.3.1 Introduction

**WHAT YOU'LL LEARN
* Introduction to data modeling
* Building an e-commerce data model
* Organizing models in apps
* Coding model classes
**

### 1.3.2 Introduction to Data Modeling

**RELATIONSHIPS
* One-to-one     1 - 1
* One-to-many    1 - *
* Many-to-many   * - *
**

### 1.3.3 Building an E-commerce Data Model

**Product**

**Cart
{Product}`*` - `*`{Cart}[created_at]
* ASSOCIATION CLASS 
	* {CartItem}[quantity]`*` - `1`{Product}
	* {CartItem}[quantity]`*` - `1`{Cart}
**

**Customer
* `*`{Customer}[name, email]`1` - `*`{Order}[placed_at]`*`
* {Order}[placed_at]`1` - `*`{OrderItem}[quantity]
* {Product}`*` - `*`{OrderItem}[quantity]
**

**Tag
{Product}`*` - `*`{Tag}[label]


### 1.3.4 Organizing Models in Apps

**MONIMAL COUPLING & HIGH COHESION (FOCUS)**

```sh
python manage.py startapp store
python manage.py startapp tags
```

```python
INSTALLED_APPS = [
	...
    'playground',
    'debug_toolbar',
    'store',
    'tags'
]
```

### 1.3.5 Creating Models

*store/models*

```python
from django.db import models
from django.db.models.fields import DateField

MAX_LENGTH = 255

class Product(models.Model):
    # sku = models.CharField(max_length=10, primary_key=True)
    title = models.CharField(max_length=MAX_LENGTH) 
    description = models.TextField()

    # 9999.99
    price = models.DecimalField(max_digits=6, decimal_places=2)
    inventory = models.IntegerField()
    last_updated = models.DateTimeField(auto_now_add=True)

class Customer(models.Model):
    first_name = models.CharField(max_length=MAX_LENGTH)
    last_name = models.CharField(max_length=MAX_LENGTH)
    email = models.CharField(unique=True)
    phone = models.CharField(max_length=MAX_LENGTH)
    birth_day = models.models.DateField(null=True)
```

### 1.3.6 Choice Field

```python
class Customer(models.Model):
    MEMBERSHIP_BRONZE = 'B'
    MEMBERSHIP_SILVER = 'S'
    MEMBERSHIP_GOLD = 'G'

    MEMBERSHIP_CHOICES = [
        (MEMBERSHIP_BRONZE, 'Bronze'),
        (MEMBERSHIP_SILVER, 'Silver'),
        (MEMBERSHIP_GOLD, 'Gold')
    ]
    first_name = models.CharField(max_length=MAX_LENGTH)
    last_name = models.CharField(max_length=MAX_LENGTH)
    email = models.CharField(unique=True)
    phone = models.CharField(max_length=MAX_LENGTH)
    birth_day = models.models.DateField(null=True)
    membership = models.CharField(max_length=1, choices=MEMBERSHIP_CHOICES, default=MEMBERSHIP_BRONZE)

class Order(models.Model):
    PAYMENT_STATUS_PENDING = 'P'
    PAYMENT_STATUS_COMPLETE = 'C'
    PAYMENT_STATUS_FAILED = 'F'

    PAYMENT_STATUS_CHOICES = [
        (PAYMENT_STATUS_PENDING, 'Pending'),
        (PAYMENT_STATUS_COMPLETE, 'Complete'),
        (PAYMENT_STATUS_FAILED, 'Failed')
    ]

    placed_at = models.DateTimeField(auto_now_add=True)
    payment_status = models.CharField(max_length=1, choices=PAYMENT_STATUS_CHOICES, default=PAYMENT_STATUS_PENDING)
```

### 1.3.7 Defining One-to-one Relationships

```python
class Address(models.Model):
    street = models.CharField(max_length=255)
    city = models.Charfield(max_length=255)
    customer = models.OneToOneField(Customer, on_delete=models.CASCADE, primary_key=True)
```

### 1.3.8 Defining a One-to-many Relationship

```python
class Address(models.Model):
    street = models.CharField(max_length=255)
    city = models.Charfield(max_length=255)
    customer = models.ForeignKey(
        Customer, primary_key=True)
```

### 1.3.9 Defining a Many-to-Many Relationship

```python
class Promotion(models.Model):
    description = models.CharField(max_length=MAX_LENGTH)
    discount = models.FloatField()

...

class Product(models.Model):
	...
    promotion = models.ManyToManyField(Promotion)
```

### 1.3.10 Resolving Circular Relationships

```python
class Collection(models.Model):
    title = models.CharField(max_length=MAX_LENGTH)
    feature_products = models.ForeignKey(
        'Product', 
        on_delete=models.SET_NULL,
         null=True,
         related_name='+')
```

### 1.3.11 Generic Relationships

```python
from django.db import models
from django.contrib.contenttypes.models import ContentType
from django.contrib.contenttypes.fields import GenericForeignKey


class Tag(models.Model):
    label = models.CharField(max_length=255)


class TaggedItem(models.Model):
    # What tag applied to what object 
    tag = models.ForeignKey(Tag, on_delete=models.CASCADE)
    # Type (product, video, article)
    # ID
    conten_type = models.ForeignKey(ContentType, on_delete=models.CASCADE)
    object_id = models.PositiveIntegerField()
    content_object = GenericForeignKey(ContentType)
```

```python
from django.db import models
from django.contrib.auth.models import User
from django.contrib.contenttypes.models import ContentType
from django.contrib.contenttypes.fields import GenericForeignKey


class LikedItem(models.Model):
    user = models.ForeignKey(User, ondelete=models.CASCADE)

    conten_type = models.ForeignKey(ContentType, on_delete=models.CASCADE)
    object_id = models.PositiveIntegerField()
    content_object = GenericForeignKey(ContentType)
```

## 1.4 Setting Up the Database

### 1.4.1 Introduction

**WHAT YOU'LL LEARN
* Creating migration
* Running migration
* Reversing migration
* Populating the database
** 

### 1.4.2 Setting Up the Database

**DATABASE ENGINS
* SQLite
* PostgreSQL
* MySQL
* MariaDB
* Oracle
**

### 1.4.3 Creating Migrations

```sh
python manage.py makemigrations
```

### 1.4.4 Running Migrations

```sh
python manage.py migrate 
```

*Install `SQLite` extension in vscode.*

*To see the SQL scripts*
```sh
python manage.py sqlmigrate store 0003
```

### 1.4.5 Customizing Database Schema

https://docs.djangoproject.com/en/3.2/ref/models/options/

```python
class Customer(models.Model):
	...
	...

    class Meta:
        db_table = 'store_customers'
        indexes = [
            models.Index(fields=['last_name', 'first_name'])
        ]
```

```sh
python manage.py makemigrations
python manage.py migrate
```

### 1.4.6 Reverting Migrations

```sh
python manage.py migrate store 0003

```sh
git reset --hard HEAD~1
# Or manually remove the code of class Meta``
```

### 1.4.7 Install MySQL

```sh
python manage.py sqlmigrate store 0003
```

### 1.4.8 Connecting to MySQL

**MYSQL CLIENTS
* MYSQL Workbench 
* TablePlus ($59)
* DataGrip ($89)
**

```sql
CREATE DATABASE storefront
```

### 1.4.9 Using MySQL in Django

```sh
pipenv install mysqlclient
```

```sh
brew install mysql
`=>
...
...
We've installed your MySQL database without a root password. To secure it run:
    mysql_secure_installation

MySQL is configured to only allow connections from localhost by default

To connect run:
    mysql -uroot

To have launchd start mysql now and restart at login:
  brew services start mysql
Or, if you don't want/need a background service you can just run:
  mysql.server start
```

```sh
pip install mysqlclient
```


```sh
$ brew services stop mysql

$ pkill mysqld

// warning: deletes all tables
$ rm -rf /usr/local/var/mysql/

$ brew postinstall mysql

$ brew services restart mysql

$ mysql -u root
Welcome to the MySQL monitor.  Commands end with ; or \g.

mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'pudong01'

mysql> exit
Bye
```

*/storefront/settings.py*
```python
# Database
# https://docs.djangoproject.com/en/3.2/ref/settings/#databases

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': "storefront",
        "HOST": "localhost",
        "USER": "root",
        "PASSWORD": "Jluo33@sh"
    }
}
```

### 1.4.10 Running Custom SQL

```sh
python manage.py makemigrations store --empty
```

```python
# Generated by Django 3.2.9 on 2021-11-09 14:47

from django.db import migrations


class Migration(migrations.Migration):

    dependencies = [
        ('store', '0003_product_slug'),
    ]

    operations = [
        migrations.RunSQL("""
            INSERT INTO store_collection (title)
            VALUES ('collection1')
        """, """
            DELETE FROM store_collection 
            WHERE title='collection1'
        """)
    ]
```

```sh
python manage.py migrate
```

*Then check the db for new data - 'collection1'*

*Revert the migration*
```sh
python manage.py migrate store 0003
```

### 1.4.11 Generating Dummy Data

https://www.mockaroo.com/

## 1.5 Django ORM

### 1.5.1 Introduction

**IN THIS SECTION
* Introduction to Django ORM
* Querying and manipulating data
* Filtering data
* Sorting data 
* Grouping data
**

### 1.5.2 Django ORM

**ORMS
* Reduce complexity in code
* Make the code more understandable
* Help us get more done in less time
**

***The best code is no code!***

*A good software engineer **delivers working** software **in time**.

*Premature optimization is the root of all evils. -Donald Knuth*

### 1.5.3 Resetting the Database

* Use `pipenv install` to create the virtual environment
* Drop the schema
* CREATE DATABASE storefront
* Use `pipenv shell` to activate the virtual environment
* run `python manage.py migrate`
* Select the schema and run the insert sql script
* run `python manage.py runserver`

### 1.5.4 Managers and QuerySets

*playground/views.py*

```python
def say_hello(request):
    query_set = Product.objects.all()

    for product in query_set:
        print(product)

    return render(request, 'hello.html', {'name': 'Mosh'}
```
*To use Django Debug Tool to view the SQL queries*


### 1.5.5 Retrieving Objects

```python
from django.shortcuts import render
from django.core.exceptions import ObjectDoesNotExist
from store.models import Product


def say_hello(request):

    try:
        product = Product.objects.get(pk=1) #primary_key
    except ObjectDoesNotExist:
        pass
    
    return render(request, 'hello.html', {'name': 'Mosh'})
```

**The `try` block is too ugly!** => 

```python
def say_hello(request):

    product = Product.objects.filter(pk=0).first()
    
    return render(request, 'hello.html', {'name': 'Mosh'})
```

*Check the existing*
```python
def say_hello(request):

    exists = Product.objects.filter(pk=0).exists()
    
    return render(request, 'hello.html', {'name': 'Mosh'})
```

### 1.5.6 Filtering Objects

*Google `queryset api` or access the link*
*https://docs.djangoproject.com/en/3.2/ref/models/querysets/*
*To check the `Filedlookups` section*


```python
def say_hello(request):
    # keyword = value
    queryset = Product.objects.filter(unit_price__range=(20, 30))
    
    return render(request, 'hello.html', {'name': 'Mosh', 'products': list(queryset)})
```

*playground/templates/hello.html*

```html
<html>
  <body>
    {% if name %}
    <h1>Hello {{ name }}</h1>
    {% else %}
    <h1>Hello World</h1>
    {% endif %}
    <ul>
      {% for product in products %}
      <li>{{ product.title }}</li>
      {% endfor %}
    </ul>
  </body>
</html>
```

```python
def say_hello(request):
    # keyword = value
    # `i` as prefix of `contains` means incase senstive
    queryset = Product.objects.filter(title__icontains="coffee") 
    # startwith
    # endwith
    
    return render(request, 'hello.html', {'name': 'Mosh', 'products': list(queryset)})
```

```python
queryset = Product.objects.filter(last_update__year=2021) 
```

### 1.5.7 Complex Lookups Using Q Objects

```python
from django.shortcuts import render
from django.db.models import Q
from django.core.exceptions import ObjectDoesNotExist
from store.models import Product


def say_hello(request):
    # keyword = value
    # queryset = Product.objects.filter(inventory__lt=10, unit_price__lt=20) 
    queryset_or = Product.objects.filter(Q(inventory__lt=10) | Q(unit_price__lt=20))
    queryset_xor = Product.objects.filter(Q(inventory__lt=10) & ~Q(unit_price__lt=20))
    
    return render(request, 'hello.html', {'name': 'Mosh', 'products': list(queryset_or)})
```

### 1.5.8  Referencing Fields using F Objects

```python
from django.shortcuts import render
from django.db.models import Q, F
from store.models import Product


def say_hello(request):

    # products: inventory = price
    queryset = Product.objects.filter(inventory=F('collection__id'))


    return render(request, 'hello.html', {'name': 'Mosh', 'products': list(queryset)})
```

### 1.5.9 Sorting

```python
def say_hello(request):

    # products: inventory = price
    # queryset = Product.objects.order_by('unit_price', '-title').reverse()
    product = Product.objects.filter(collection_id=1).order_by('unit_price')[0]
    product = Product.objects.latest('unit_price')
    return render(request, 'hello.html', {'name': 'Mosh', 'product': product})
```

### 1.5.10 Limiting Results

```python
def say_hello(request):

    queryset = Product.objects.all()[5:10]
    return render(request, 'hello.html', {'name': 'Mosh', 'products': list(queryset)})
```

### 1.5.11 Selecting Fields to Query

```python
def say_hello(request):

    queryset = Product.objects.values("id", "title", "collection__title")
    return render(request, 'hello.html', {'name': 'Mosh', 'products': list(queryset)})
```
=>
```json
{'id': 2, 'title': 'Island Oasis - Raspberry', 'collection__title': 'Beauty'}
{'id': 3, 'title': 'Shrimp - 21/25, Peel And Deviened', 'collection__title': 'Beauty'}
{'id': 12, 'title': 'Beer - Alexander Kieths, Pale Ale', 'collection__title': 'Beauty'}
{'id': 17, 'title': 'Salt - Rock, Course', 'collection__title': 'Beauty'}
{'id': 20, 'title': 'Cheese - Parmesan Cubes', 'collection__title': 'Beauty'}
{'id': 24, 'title': 'Chinese Foods - Pepper Beef', 'collection__title': 'Beauty'}
{'id': 26, 'title': 'Tendrils - Baby Pea, Organic', 'collection__title': 'Beauty'}
{'id': 34, 'title': 'Hinge W Undercut', 'collection__title': 'Beauty'}
...
...
```

```python
def say_hello(request):

    queryset = Product.objects.values_list("id", "title", "collection__title")
    return render(request, 'hello.html', {'name': 'Mosh', 'products': list(queryset)})
```
=>
```python
(2, 'Island Oasis - Raspberry', 'Beauty')
(3, 'Shrimp - 21/25, Peel And Deviened', 'Beauty')
(12, 'Beer - Alexander Kieths, Pale Ale', 'Beauty')
(17, 'Salt - Rock, Course', 'Beauty')
(20, 'Cheese - Parmesan Cubes', 'Beauty')
(24, 'Chinese Foods - Pepper Beef', 'Beauty')
(26, 'Tendrils - Baby Pea, Organic', 'Beauty')
(34, 'Hinge W Undercut', 'Beauty')
```

**Exercises**
*Select products that have been ordered and sort them by title*

```python
def say_hello(request):

    queryset = Product.objects.filter(id__in=OrderItem.objects.values('product_id').distinct()).order_by('title')
    return render(request, 'hello.html', {'name': 'Mosh', 'products': list(queryset)})
```

### 1.5.12 Deferring Fields

***Be carefule to use `only` and `defer` for the corresponding fields.***

```python
def say_hello(request):
    
    # queryset = Product.objects.only('id', 'title)    
    queryset = Product.objects.defer('description')
    return render(request, 'hello.html', {'name': 'Mosh', 'products': list(queryset)})
```

### 1.5.13 Selecting Related Objects

```python
def say_hello(request):
    
    # queryset = Product.objects.all()  # > 1000 queries 
    # select_related(1)
    # queryset = Product.objects.select_related('collection').all() # 3 queries
    
    # prefecth_related(n)
    queryset = Product.objects.prefetch_related('promotions').all().select_related('collection')
    
    return render(request, 'hello.html', {'name': 'Mosh', 'products': list(queryset)})
```

**Get the last 5 orders with their customer 
and items (incl product)**


```python
def say_hello(request):
    
    queryset = Order.objects.select_related(
        'customer').prefetch_related('orderitem_set__product').order_by('-placed_at')[:5]
    
    return render(request, 'hello.html', {'name': 'Mosh', 'orders': list(queryset)})
```

### 1.5.14 Aggregating Objects


```python
from django.shortcuts import render
from django.db.models.aggregates import Count, Min
from store.models import Product


def say_hello(request):
    
    result = Product.objects.filter(collection__id=1).aggregate(
        count=Count('id'), 
        min_price=Min('unit_price'))
    
    return render(request, 'hello.html', {'name': 'Mosh', 'result': result})
```

### 1.5.15 Annotating Objects

```python
from django.shortcuts import render
from django.db.models import Value, F
from store.models import Product, Customer


def say_hello(request):
    
    # queryset = Customer.objects.annotate(is_new=Value(True))
    queryset = Customer.objects.annotate(new_id=F('id') + 1)
    
    return render(request, 'hello.html', {'name': 'Mosh', 'products': list(queryset)})
```

### 1.5.16 Calling Database Functions

*Google `django database functions`*

```python
from django.shortcuts import render
from django.db.models import Value, F, Func
from django.db.models.functions import Concat
from store.models import Product, Customer


def say_hello(request):
    
    # queryset = Customer.objects.annotate(
    #     # CONCAT
    #     full_name=Func(F('first_name'), Value(' '), F('last_name'), function='CONCAT')
    # )

    queryset = Customer.objects.annotate(
        # CONCAT
        full_name=Concat('first_name', Value(' '), 'last_name')
    )
    
    return render(request, 'hello.html', {'name': 'Mosh', 'products': list(queryset)})
```

### 1.5.17 Grouping Data

```python
from django.shortcuts import render
from django.db.models import Value, F, Func, Count
from django.db.models.functions import Concat
from store.models import Product, Customer


def say_hello(request):

    queryset = Customer.objects.annotate(
        orders_count=Count('order')
    )
    
    return render(request, 'hello.html', {'name': 'Mosh', 'products': list(queryset)})
```

### 1.5.18 Working with Expression Wrappers

**Expression
* Value
* F
* Func
* Aggregate
* *ExpressionWrapper*
**

```python
from django.db.models.fields import DecimalField
from django.shortcuts import render
from django.db.models import Value, F, Func, ExpressionWrapper
from django.db.models.functions import Concat
from store.models import Product, Customer


def say_hello(request):

    discounted_price = ExpressionWrapper(
        F('unit_price') * 0.8, output_field=DecimalField())

    queryset = Product.objects.annotate(
        discounted_price=discounted_price
    )
    
    return render(request, 'hello.html', {'name': 'Mosh', 'products': list(queryset)})
```

#### 1.5.18.1 Annotating Exercises - Customers with their last order ID

```python
    queryset = Customer.objects.annotate(
        last_order_id=Max('order__id')
    )
```

#### 1.5.18.2 Annotating Exercises - Collections and count of their products 

```python
    queryset = Collection.objects.annotate(
        product_count=Count('product')
    )
```

#### 1.5.18.3 Annotating Exercises - Customers with more than 5 orders 

```python
    queryset = Customer.objects.annotate(
        orders_count=Count('order')
    ).filter(orders_count__gt=5)
```

#### 1.5.18.4 Annotating Exercises - Customers and the total amount they’ve spent


```python
    queryset = Customer.objects.annotate(
        total_spent=Sum(
            F('order__orderitem__unit_price') * 
            F('order__orderitem__quantity'))
    )
```

#### 1.5.18.5 Annotating Exercises - Top 5 best-selling products and their total sales 

```python
    queryset = Product.objects.annotate(
        total_sales=Sum(
            F('orderitem__unit_price') * 
            F('orderitem__quantity'))
    ).order_by('-total_sales')[:5]
```

### 1.5.19 Querying Generic Relationships

```python
from django.db.models.fields import DecimalField
from django.shortcuts import render
from django.contrib.contenttypes.models import ContentType
from store.models import Product
from tags.models import TaggedItem

def say_hello(request):

    content_type = ContentType.objects.get_for_model(Product)

    queryset = TaggedItem \
        .objects.select_related('tag') \
        .filter(
        content_type=content_type,
        object_id=1
    )
    
    return render(request, 'hello.html', {'name': 'Mosh', 'tags': list(queryset)})
```

### 1.5.20 Custom Managers

*tags/models.py*
```python
class TaggedItemManager(models.Manager):
    def get_tags_for(self, obj_type, obj_id):
        content_type = ContentType.objects.get_for_model(obj_type)

        return TaggedItem \
            .objects.select_related('tag') \
            .filter(
            content_type=content_type,
            object_id=obj_id
        )
```

*Insert `objects = TaggedItemManager()` into `TaggedItem` class then*
```python
class TaggedItem(models.Model):
    objects = TaggedItemManager()
    tag = models.ForeignKey(Tag, on_delete=models.CASCADE)
    content_type = models.ForeignKey(ContentType, on_delete=models.CASCADE)
    object_id = models.PositiveIntegerField()
    content_object = GenericForeignKey()
```

*playground/views.py*
```python
from django.shortcuts import render
from store.models import Product
from tags.models import TaggedItem

def say_hello(request):

    queryset = TaggedItem.objects.get_tags_for(Product, 1)
    
    return render(request, 'hello.html', {'name': 'Mosh', 'tags': list(queryset)})
```

### 1.5.21 Understanding QuerySet Cache

```python
def say_hello(request):

    queryset = Product.objects.all()
    queryset[0]
    list(queryset)
```

### 1.5.22 Creating Objects

```python
from django.shortcuts import render
from store.models import Collection, Product


def say_hello(request):

    collection = Collection()
    collection.title = 'Video Games'
    collection.featured_product = Product(pk=1)
    collection.save()
    
    return render(request, 'hello.html', {'name': 'Mosh'})
```
=>
```sql
INSERT INTO `store_collection` (`title`, `featured_product_id`)
VALUES ('Video Games', 1)
```

### 1.5.23 Updating Objects

```python
from django.shortcuts import render
from store.models import Collection, Product


def say_hello(request):

    collection = Collection(pk=11)
    collection.title = 'Games'
    collection.featured_product = None
    collection.save()
    
    return render(request, 'hello.html', {'name': 'Mosh'})
```
=>
```sql
INSERT INTO `store_collection` (`title`, `featured_product_id`)
VALUES ('Video Games', 1)
```

```python
def say_hello(request):

    collection = Collection(pk=11)
    collection.featured_product = None
    collection.save()
```
=> **`SET `title` = ''` causes data loss!!!**
```sql
UPDATE `store_collection` SET `title` = '', `featured_product_id` = NULL WHERE `store_collection`.`id` = 11
```
*Because django will implictly implement `collection.title = ''`*

***Correct Implementation***
```python
Collection.objects.filter(pk=11).update(featured_product=None)
```

### 1.5.24 Deleting Objects

```python
    collection = Collection(pk=11)
    collection.delete()

    # Collection.objects.filter(id__gt=5).delete()
```

### 1.5.25 Transactions

```python
    order = Order()
    order.customer_id = 1
    order.save()

    item = OrderItem()
    item.order = order
    item.product_id = 1
    item.quantity = 1
    item.unit_price = 10
    item.save()
```
*-> Wrapp this actions into one transaction*

```python
from django.shortcuts import render
from django.db import transaction
from store.models import Order, OrderItem


def say_hello(request):

    #...

    with transaction.atomic():
        order = Order()
        order.customer_id = 1
        order.save()

        item = OrderItem()
        item.order = order
        item.product_id = 1
        item.quantity = 1
        item.unit_price = 10
        item.save()
    
    return render(request, 'hello.html', {'name': 'Mosh'})
```

*Refresh the page and use this script to check the db*
```sql
select *
from store_order
order by id desc
```

### 1.5.26 Executing Raw SQL Queries

```python
from django.shortcuts import render
from store.models import Product


def say_hello(request): 

    queryset = Product.objects.raw('SELECT id, title FROM store_product')

    return render(request, 'hello.html', {'name': 'Mosh', 'results': list(queryset)})
```
***Use it when it is needed!***
```python
from django.shortcuts import render
from django.db import connection
from store.models import Product


def say_hello(request): 
    with connection.cursor() as cursor:
        cursor.execute('')
        # cursor.callproc('get_customers', [1, 2, 'a'])

    return render(request, 'hello.html', {'name': 'Mosh', 'results': list(queryset)})
```


## 1.6 The Admin Site

### 1.6.1 Introduction

**IN THIS SECTION
* Customizing the admin interface
* Adding computed columns
* Loading related objects
* Adding search & filters
* Implementing custom actions
* Adding data validation
**

### 1.6.2 Setting Up the Admin Site

*http://localhost:8000/admin/*

```sh
python manage.py createsuperuser
`=>
Username (leave blank to use 'mac'): admin
Email address: lawjune@163.com
Password:
Password (again):
This password is too short. It must contain at least 8 characters.
This password is too common.
This password is entirely numeric.
Bypass password validation and create user anyway? [y/N]: y
Superuser created successfully.
```

*Add 'django.contrib.sessions' in /storefront/settings.py INSTALLED_APPS*

```sh
python manage.py changepassword admin
```

*To make the website more meeaningful*
*/storefront/urls.py to add these two lines anc refresh the web page*

```python
admin.site.site_header = 'Store Admin'
admin.site.index_title = 'Admin'
```

### 1.6.3 Registering Models

*/store/admin.py*
```python
from django.contrib import admin
from . import models

admin.site.register(models.Collection)
```

*/store/models.py -> Collection*
*To override the magic method __str__*
*To add the `Meta` class for sorting*
```python
class Collection(models.Model):
    title = models.CharField(max_length=255)
    featured_product = models.ForeignKey(
        'Product', on_delete=models.SET_NULL, null=True, related_name='+')
    def __str__(self) -> str:
        return self.title

    class Meta:
        ordering = ['title']
```

***Register the `Product` with the same process***

### 1.6.4 Customizing the List Page

*Google `Django ModelAdmin`*

```python
from django.contrib import admin
from . import models

@admin.register(models.Product)
class ProductAdmin(admin.ModelAdmin):
    list_display = ['title', 'unit_price']
    list_editable = ['unit_price']
    list_per_page = 10

@admin.register(models.Customer)
class CustomerAdmin(admin.ModelAdmin):
    list_display = ['first_name', 'last_name', 'membership']
    list_editable = ['membership']
    list_per_page = 10

admin.site.register(models.Collection)
```

### 1.6.5 Adding Computed Columns

*Revise the ProductAdmin class*
```python
class ProductAdmin(admin.ModelAdmin):
    list_display = ['title', 'unit_price', 'inventory_status']
    list_editable = ['unit_price']
    list_per_page = 10

    @admin.display(ordering='inventory')
    def inventory_status(self, product):
        if product.inventory < 10:
            return 'LOW'
        return 'OK'
```

### 1.6.6 Selecting Related Objects

*Add these to `Customer` model*
```python

    def __str__(self):
        return f'{self.first_name} {self.last_name}'

    class Meta:
        ordering = ['first_name', 'last_name']
```

```python
from django.contrib import admin
from . import models

@admin.register(models.Product)
class ProductAdmin(admin.ModelAdmin):
    list_display = ['title', 'unit_price', 'inventory_status', 'collection_title']
    list_editable = ['unit_price']
    list_per_page = 10
    list_select_related = ['collection']

    def collection_title(self, product):
        return product.collection.title

    @admin.display(ordering='inventory')
    def inventory_status(self, product):
        if product.inventory < 10:
            return 'LOW'
        return 'OK'

@admin.register(models.Order)
class OrderAdmin(admin.ModelAdmin):
    list_display = ['id', 'placed_at', 'customer']

@admin.register(models.Customer)
class CustomerAdmin(admin.ModelAdmin):
    list_display = ['first_name', 'last_name', 'membership']
    list_editable = ['membership']
    list_per_page = 10

admin.site.register(models.Collection)
```

### 1.6.7 Overriding the Base QuerySet

```python
@admin.register(models.Collection)
class CollectionAdmin(admin.ModelAdmin):
    list_display = ['title', 'products_count']

    @admin.display(ordering='products_count')
    def products_count(self, collection):
        return collection.products_count

    def get_queryset(self, request: HttpRequest) -> QuerySet:
        return super().get_queryset(request).annotate(
            products_count=Count('product')
        )
```

### 1.6.8 Providing Links to Other Pages

```python
from django.utils.html import format_html, urlencode
```
```python
@admin.register(models.Collection)
class CollectionAdmin(admin.ModelAdmin):
    list_display = ['title', 'products_count']

    @admin.display(ordering='products_count')
    def products_count(self, collection):
        url = (
            reverse('admin:store_product_changelist') 
            + '?'
            + urlencode({
                'collection__id': str(collection.id)
            })
            )
        return format_html('<a href="{}">{}</a>', url, collection.products_count)
        # return collection.products_count

    def get_queryset(self, request: HttpRequest) -> QuerySet:
        return super().get_queryset(request).annotate(
            products_count=Count('product')
        )
```

### 1.6.9 Adding Search to the List Page

```python
@admin.register(models.Customer)
class CustomerAdmin(admin.ModelAdmin):
    list_display = ['first_name', 'last_name', 'membership']
    list_editable = ['membership']
    list_per_page = 10
    ordering = ['first_name', 'last_name']
    search_fields = ['first_name__istartswith', 'last_name__istartswith']
```

### 1.6.10 Adding Filtering to the List Page

```python
class InventoryFilter(admin.SimpleListFilter):
    title = 'inventory'
    parameter_name = 'inventory'

    def lookups(self, request, model_admin):
        return [
            ('<10', 'Low')
        ]

    def queryset(self, request, queryset: QuerySet):
        if self.value() == '<10':
            return queryset.filter(inventory__lt=10)

@admin.register(models.Product)
class ProductAdmin(admin.ModelAdmin):
    list_display = ['title', 'unit_price', 'inventory_status', 'collection_title']
    list_editable = ['unit_price']
    list_filter = ['collection', 'last_update', InventoryFilter]
    list_per_page = 10
    list_select_related = ['collection']

    def collection_title(self, product):
        return product.collection.title

    @admin.display(ordering='inventory')
    def inventory_status(self, product):
        if product.inventory < 10:
            return 'LOW'
        return 'OK'
```

### 1.6.11 Creating Custom Actions

```python
from django.contrib import admin, messages
......

@admin.register(models.Product)
class ProductAdmin(admin.ModelAdmin):
    actions = ['clear_inventory']

    ......

    @admin.action(description="Clear inventory")
    def clear_inventory(self, request, queryset):
        updated_count = queryset.update(inventory=0)
        self.message_user(
            request,
            f'{updated_count} products are succssfully updated.',
            messages.ERROR
        )
```

### 1.6.12 Customizing Forms

```python
@admin.register(models.Product)
class ProductAdmin(admin.ModelAdmin):
    fields = ['title', 'slug']
    exclude = ['promotions']
    readonly_fields = ['title']
    prepopulated_fields = {
        'slug': ['title']
    }
```

*Insert the autocomplete_fields, then*
```python
@admin.register(models.Product)
class ProductAdmin(admin.ModelAdmin):
    autocomplete_fields = ['collection']
```

*Terminal output:
ERRORS:
<class 'store.admin.ProductAdmin'>: (admin.E040) CollectionAdmin must define "search_fields", because it's referenced by ProductAdmin.autocomplete_fields.
*

```python
@admin.register(models.Collection)
class CollectionAdmin(admin.ModelAdmin):
    list_display = ['title', 'products_count']
    search_fields = ['title']
```

### 1.6.13 Adding Data Validation

*Modify the data model*
```python
class Product(models.Model):
    ...
    description = models.TextField(null=True)
    ...
```

```sh
python manage.py makemigrations
python manage.py migrate
```

*The `description` field is still required, because the above code only applied to the database.*

```python
class Product(models.Model):
    ...
    description = models.TextField(null=True, blank=True)
    ...
```

```python
from django.core.validators import MinValueValidator
...
class Product(models.Model):
    ...
    unit_price = models.DecimalField(
        max_digits=6, 
        decimal_places=2,
        validators=[MinValueValidator(1)]
        )
    ...
    promotions = models.ManyToManyField(Promotion, blank=True)
```
*Google `django validators`*


### 1.6.14 Editing Children Using Inlines

```python
class OrderItemInline(admin.TabularInline):
    autocomplete_fields = ['product']
    min_num = 1
    max_num = 10
    model = models.OrderItem
    extra = 0

@admin.register(models.Order)
class OrderAdmin(admin.ModelAdmin):
    autocomplete_fields = ['customer']
    inlines = [OrderItemInline]
    list_display = ['id', 'placed_at', 'customer']
```

**Try the `StackedInline`**
```python
class OrderItemInline(admin.StackedInline):
```

### 1.6.15 Using Generic Relations

*/tags/admin.py*
```python
from django.contrib import admin
from .models import Tag
# Register your models here.
admin.site.register(Tag)
```

*/tags/model.py*
```python
class Tag(models.Model):
    label = models.CharField(max_length=255)

    def __str__(self) -> str:
        return self.label
```

*/store/admin.py*
```python
from django.contrib.contenttypes.admin import GenericTabularInline
from tags.models import TaggedItem
...

class TagInline(GenericTabularInline):
    autocomplete_fields = ['tag']
    model = TaggedItem

@admin.register(models.Product)
class ProductAdmin(admin.ModelAdmin):
    ...
    inlines = [TagInline]
    ...
...
```

*/tags/admin.py*
```python
@admin.register(Tag)
class TagAdmin(admin.ModelAdmin):
    search_fields = ['label']
```

### 1.6.16 Extending Pluggable Apps

**How to decouple:
```python
from tags.models import TaggedItem
```
**

```sh
python manage.py startapp store_custom
```

*Move the TagInline from /store/admin.py to /store_custom/admin.py*
```python
from django.contrib import admin
from django.contrib.contenttypes.admin import GenericTabularInline
from store.admin import ProductAdmin
from store.models import Product
from tags.models import TaggedItem

class TagInline(GenericTabularInline):
    autocomplete_fields = ['tag']
    model = TaggedItem

class CustomerProductAdmin(ProductAdmin):
    inlines = [TagInline]

admin.site.unregister(Product)
admin.site.register(Product, CustomerProductAdmin)
```

**Remove the `store_custom` in /storefront/settings.py if it's no needed for configuration.**

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.sessions',
    'django.contrib.contenttypes',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'playground',
    'debug_toolbar',
    'store',
    # 'store_custom',
    'tags',
    'likes'
]
```







