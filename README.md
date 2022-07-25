# Creamos el entorno virtual
```
virtualenv env --python=python3
source env/bin/activate
pip freeze
```
# Instalamos Django
```
pip install django
```

# .env
```
Instalamos la libreria
$ pip install python-decouple

En el config
from decouple import config
SECRET_KEY = config("SECRET_KEY", default='')

Creamos el .env
SECRET_KEY=HELLO
```

# Django Ayuda
```
python3 vaxiproject/manage.py help
```

# Crear Proyecto
```
django-admin startproject demo
python3 vaxiproject/manage.py runserver
```

# Migraciones
```
python3 manage.py migrate
python3 manage.py makemigrations
python manage.py runserver
```

# Crear apps
```
python3 demo/manage.py startapp usuarios
django-admin startapp front app/front
django-admin startapp chat app/chat
```

# Comandos Varios
```
$ python3 -m venv env
$ source ./env/bin/activate
$ pip install django
$ pip freeze
$ django-admin startproject marlonapps .
$ django-admin startapp base
$ python3 manage.py runserver
$ pip freeze > requirements.txt
$ mkdir apps
$ python manage.py collectstatic
$ pip freeze > requirements.txt
```
