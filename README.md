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
python3 vaxiproject/manage.py startapp usuarios
```
