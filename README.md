Run Django used nginx.
 sudo apt update 
 sudo apt install python3-pip python3-dev libpq-dev postgresql postgresql-contrib nginx curl

Create database and table 
sudo -u postgres psql 
CREATE DATABASE sortproject;
CREATE USER postgres WITH PASSWORD 'postgres';
ALTER ROLE clouduser SET client_encoding TO 'utf8';

For create virtual machine 
sudo -H pip3 install --upgrade pip
sudo -H pip3 install virtualenv
mkdir ~/sortproject
cd ~/sortproject
virtualenv sortenv

source sortenv/bin/activate
pip install django gunicorn psycopg2-binary

Create project 
django-admin.py startproject sortproject ~/sortproject
nano ~/sortproject/sortproject/settings.py

Connect with database
DATABASES = {
'default': {
'ENGINE': 'django.db.backends.postgresql_psycopg2',
'NAME': 'sortproject',
'USER': 'sortuser',
'PASSWORD': 'password',
'HOST': 'localhost',
'PORT': '',
}
}
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static/')

Finish
~/sortproject/manage.py makemigrations
~/sortproject/manage.py migrate

~/sortproject/manage.py createsuperuser 
~/cloudproject/manage.py collectstatic
sudo ufw allow 8000 # port for start project
~/cloudproject/manage.py runserver 


Import an existing, unversioned code project into Bitbucket Server
git remote add origin git@bitbucket.org:m_martsul/intericstesttask.git
git push -u origin master
