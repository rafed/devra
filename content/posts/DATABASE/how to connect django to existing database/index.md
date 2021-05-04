---
title: How to Connect Django to an Existing Legacy Database
date: 2021-04-05
tags: [database, programming, python]
image: "image.png"
---

What if you needed to connect a django project with an exiting database that already contains data? In this tutorial we will learn how to connect an existing MySQL database to a django project.

## Get an existing database

If don't have an existing database to play with, you can get one at [mysqltutorial.org](https://www.mysqltutorial.org/mysql-sample-database.aspx/)

## Import the data to MySQL

If you don't have MySQL installed, set it up now. After setup, import the data from the downloaded SQL file.

```bash
$ mysql -u user -p < mysqlsampledatabase.sql
# you may need to enter password
```

## Setup Django project to work with MySQL

Install mysql driver for python.
```bash
$ pip install pymysql
```

Then in **settings.py** of the project, import and use pymysql.
```python
import pymysql
pymysql.install_as_MySQLdb()
```

Additionally, enter the following conigurations for mysql in **settings.py**.

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'classicmodels', # database name
        'USER': 'user',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

## Create the Django models from MySQL

The above below will produce django models in **models.py** from tables present in MySQL. 

```bash
$ python manage.py inspectdb > models.py
```

The output will be somewhat like this.

```python
class Customers(models.Model):
    customernumber = models.IntegerField(db_column='customerNumber', primary_key=True)  # Field name made lowercase.
    customername = models.CharField(db_column='customerName', max_length=50)  # Field name made lowercase.
    ... 

    class Meta:
        managed = True
        db_table = 'customers'


class Employees(models.Model):
    employeenumber = models.IntegerField(db_column='employeeNumber', primary_key=True)  # Field name made lowercase.
    lastname = models.CharField(db_column='lastName', max_length=50)  # Field name made lowercase.
    ...

    class Meta:
        managed = False
        db_table = 'employees'
```

Finally, migrate the models.

```bash
$ python run manage.py migrate
```

## Create app and use the models

Now that the django model bindings are ready let's create an app and test drive it.

Create an app-

```bash
$ python manage.py startapp legacy
```

In this new app copy the **models.py** created in the previous section.

Now let's create a view to use the models.

```python
from django.http import HttpResponse

from .models import Customers

def index(request):
    customers = Customers.objects.all()[:5]
    output = '<br>'.join([c.customername for c in customers])
    return HttpResponse(output)
```

Let's configure the urls in **legacy/urls.py**.

```python
from django.urls import path
from . import views

app_name = 'legacy'
urlpatterns = [
    path('customers/', views.index, name='customers'),
]
```

And also in the root project **urls.py**.

```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('legacy/', include('legacy.urls')),
]
```

Now visit the page **localhost:8000/legacy/customers/**, you should see data retrieved from the legacy tables.

```txt
Atelier graphique
Signal Gift Stores
Australian Collectors, Co.
La Rochelle Gifts
Baane Mini Imports
```

Awesome! Now we can work in django with legacy databases!

## Modifying database tables

Legacy tables are not permitted to be modified by default. But they can be modified if needed. First set **managed=True** in sub Meta classes of classes you want to modify. And then, add the new field you want.

```python
class Customers(models.Model):
    customernumber = models.IntegerField(db_column='customerNumber', primary_key=True)  # Field name made lowercase.
    customername = models.CharField(db_column='customerName', max_length=50)  # Field name made lowercase.
    demo = models.CharField(db_column='customerName', max_length=50, blank=True, null=True) # NEW FIELD
    ... 

    class Meta:
        managed = True
        db_table = 'customers'
```

Now, make the migrations file.

```bash
$ python manage.py makemigrations
```

Since the tables already exist, we need a fake migration.

```bash
$ python manage.py migrate --fake
```

Voila! Now the new table field should be added!