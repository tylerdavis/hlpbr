#HLPBR/Django/Heroku - Install Notes
##Create your project
1. Create the project folder  
`mkdir hlprb && cd hlpbr`  

2. Build the virtualenv in your project directory  
`virtualenv --no-site-packages .`

3. Activate the venv path  
`source bin/activate`

4. Install required packages  
`pip install Django django-celery django-kombu psycopg2 gunicorn pil`

5. Create the requirements.txt file  
`pip freeze > requirements.txt`

6. Build the project  
`django-admin.py startproject hlpbr`

7. Update `INSTALLED_APPS` in your project's settings.py

```
'gunicorn',
'djcelery',
'djkombu',
```
8. Prepend the following SITE_ROOT configuration to your project's
   settings.py

'''python
import os

SITE_ROOT = os.path.dirname(os.path.realpath(__file__))
'''

8. Append the following Celery configuration to your project's
   settings.py

```python
import djcelery
djcelery.setup_loader()
BROKER_BACKEND = "djkombu.transport.DatabaseTransport"
CELERY_RESULT_DBURI = DATABASES['default']
```

8. Create and populate the Procfile
`web: python hlpbr/manage.py run_gunicorn -b "0.0.0.0:$PORT" -w 3`

9. Create .gitignore and include the following:

```
*.pyc
*.swp
```

10. Run locally
`foreman start`

10. Initialize repository and commit
`git init`
`git add .`
`git commit -m "hlpbr"

11. Deploy to Heroku
`heroku create --stack cedar`
`git push heroku master`
