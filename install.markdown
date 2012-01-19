#HLPBR/Django/Heroku - Install Notes
1. Create the project folder  
`mkdir hlprb && cd hlpbr`  
2. Build the virtualenv in your project directory  
`virtualenv --no-site-packages .`
3. Activate the venv path  
`source bin/activate`
4. Install required packages  
`pip install Django psycopg2 pil`
5. Create the requirements.txt file  
`pip freeze > requirements.txt`
6. Build the project  
`django-admin.py startproject hlpbr`
7. Create .gitignore and include the following:
    venv
    *.pyc
