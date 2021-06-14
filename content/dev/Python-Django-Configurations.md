---
title: "Python Django Configurations"
date: 2021-06-11T01:41:25+09:00
draft: false
---

> This post includes a brief summary of how-to setup a proper configuration for migrating wordpress-based webservice to django for the following website [REITSKorea](https://reitskorea.co.kr).
> References come mostly from: [Nomadcoders](https://nomadcoders.com) and my personal researches throughout the internet.
---
<br />
<br />


## 1. pipenv & install django
*pipenv is a package + virtual environment manager. To simply put: it's pip + virtualenv combined.*  
 <br />

#### 1-1. Install pipenv  with:  
> `pip install pipenv` or `brew install pipenv`
#### 1-2. Enter the pipenv shell & install Django  

>`pipenv shell`  
>`pipenv install django`

#### 1-3. Start a Django project with configuration options
> `django startproject config`

Then change the directory structure: gather all the configuration files (settings.py, wsgi.py ... etc) in one single 'config' folder in the parent directory.


<br />
<br />
<br />

## 2. Changing the default DB(sqlite3) to postgresql
*Django requires a module called psycopg2 as an adapter to connect to postgresql DB.*  
<br />

#### 2-1. Install psycopg2 with:
> `pipenv install psycopg2`

if the above command doesn't work & Prints out an error, try the binary version of the psycopg2:  
> `pipenv install psycopg2-binary`

**As of Jun 11. 2021**,  

The current version of psycopg2-binary(2.8.6) happened to have dependency errors in my M1 Mac(Big Sur) local environement

So, I installed the version in development at local environement without locking it to pipfile:

> `pipenv install -i https://test.pypi.org/simple psycopg2-binary==2.9.0.dev0 --skip-lock`

Then manually changed the pipfile's psycopg2 version to "2.8.6" for deployment purposes.  

<br />
<br />
#### 2-2. postgresql create local DB  

After successfully installing psycopg2 module, you need to create a local postgresql DB for django.

if you haven't installed postgresql, install it via command:
> `brew install postgresql`

After, get inside the postgresql console by command:
> `psql`

Then create a DB with a command:  
> `CREATE DATABASE {db_name} WITH OWNER = {user_name};`

For example:  
> `CREATE DATABASE reitskorea WITH OWNER = woogieboogie;`

*For above example, if you don't have a user yet, make sure you create a user and then create a postgresql db with it.*

<br />
<br />
<br />

## 3. Change settings.py
*modify settings.py in order to connect to created postgresql DB*

<br />
<br />

#### 3-1. Change DATABASE settings in settings.py
<br />
from:
```
# config/settings.py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```
to:
```
# config/settings.py
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'dbname',
        'USER': 'username',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '',
    }
}   
```
<br />

#### 3-2. DB Migrate
migrate your model to the postgresql DB by:
> `python manage.py migrate`

<br />
<br />
<br />

## 4. Optional: seperating working environments
*Sometimes, you want to seperate working environments to manage your project/product with more stability. In this project, I've seperated the configuration file into three seperate environments: local, test, and production environment*

<br />

#### 4-1. directory settings
Create a settings folder, then create __init__.py, base.py, local.py, test.py, and production.py inside it.

The resulting config folder directory structure should be as follows:
```
project
│   README.md
│   ...
│
└───config
│   │   wsgi.py
│   │   urls.py
│   │   ...
│   │
│   └───settings
│       │   __init__.py
│       │   base.py
│       │   local.py
│       │   test.py
│       │   production.py
│   
...
```
<br />


#### 4-2. How to seperate in each environment
<br />

**In base.py**, You want to place the common configuration settings for the project such as application settings / admin settings.. etc
```
# config/settings/base.py

DJANGO_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]

PROJECT_APPS = [
    "core.apps.CoreConfig",
    "users.apps.UsersConfig",
    "reits.apps.ReitsConfig",
    "sectors.apps.SectorsConfig",
]
...
```
<br />

**In local.py**  
You want to place local configuration settings where you will be debugging and building the project. Good examples would be DEBUG=TRUE options, ALLOWED_HOSTS options and local DB settings... etc

```
# config/settings/local.py

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'reitskorea',
        'USER': 'woogieboogie',
        'PASSWORD': 'password',
        'HOST': 'localhost',
        'PORT': '',
    }
}

ALLOWED_HOSTS = []
```

<br />

**In test.py**  
You want to place test-level configuration settings. 
I usually have the same settings as production since test-level service is a pre-flight test just before deploying the service to the production environment.


<br />

**In production.py**  
You want to place production-level configuration settings for deployment and production.  
Examples of this would be static file locations, and allowed host lists in production environment.  

You do not want to explicitly have sensitive key-values stored in this file.  (ex. AWS passwords, DB passwords, etc..)  

**MAKE SURE TO USE SEPERATE ENVIRONMENT** or store them somewhere else hidden datas.

```
# config/settings/production.py

AWS_STORAGE_BUCKET_NAME = "nomad-django-production-bucket"
AWS_LOCATION = 'static'
AWS_REGION = 'ap-northeast-2'
AWS_S3_CUSTOM_DOMAIN = f"{AWS_STORAGE_BUCKET_NAME}.s3.{AWS_REGION}.amazonaws.com"

STATIC_URL = f"https://{AWS_S3_CUSTOM_DOMAIN}/{AWS_LOCATION}/"
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static'),
]

MEDIA_URL = "/media/"
MEDIA_ROOT = os.path.join(BASE_DIR, "uploads")


sentry_sdk.init(
    dsn=os.environ.get("SENTRY_URL"),
    integrations=[DjangoIntegration()],

    # Set traces_sample_rate to 1.0 to capture 100%
    # of transactions for performance monitoring.
    # We recommend adjusting this value in production.
    traces_sample_rate=1.0,

    # If you wish to associate users to errors (assuming you are using
    # django.contrib.auth) you may enable sending PII data.
    send_default_pii=True
    )
```

<br />
<br />
<br />