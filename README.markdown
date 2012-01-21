@TODO - Document bootstrap integration  
@TODO - Document static file handling (local & s3 deployed)

#Django/Heroku/Gunicorn/Bootstrap - Install Notes
##Create your project
###Create the project folder  
`mkdir hlprb && cd hlpbr`  

###Build the virtualenv in your project directory  
`virtualenv --no-site-packages .`

###Activate the venv path  
`source bin/activate`

###Install required packages  
`pip install Django django-celery django-kombu psycopg2 gunicorn pil ipython`

###Create the requirements.txt file  
`pip freeze > requirements.txt`

###Build the project  
`django-admin.py startproject hlpbr`

###Create templates and static directories  
`cd hlpbr && mkdir templates && mkdir static`

### @TODO - Bootstrap integration goes here

###Update _INSTALLED_APPS_ in your project's settings.py

```
'gunicorn',
'djcelery',
'djkombu',
```

###Prepend the following SITE_ROOT configuration to your project's
   settings.py

```python
import os

SITE_ROOT = os.path.dirname(os.path.realpath(__file__))
```

@TODO - Static file handling docs go here

###Append the following Celery configuration to your project's settings.py

```python
import djcelery
djcelery.setup_loader()
BROKER_BACKEND = "djkombu.transport.DatabaseTransport"
CELERY_RESULT_DBURI = DATABASES['default']
```

###Append the following local settings import to your settings.py

`from settings_local import *` 

###Create settings_local.py in your SITE_ROOT to use

```python
DEBUG = True
TEMPLATE_DEBUG = DEBUG

# No emails while developing
ADMINS = ()
MANAGERS = ADMINS
```

###Create and populate the Procfile
`web: python hlpbr/manage.py run_gunicorn -b "0.0.0.0:$PORT" -w 3`

###Create .gitignore and include the following:

```
[Project_File]/settings_local.py
*.pyc
*.swp
```

###Run locally
`foreman start`

###Initialize repository and commit
`git init`
`git add .`
`git commit -m "hlpbr"`

###Deploy to Heroku
`heroku create --stack cedar`
`git push heroku master`
