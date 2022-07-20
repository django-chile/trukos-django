# Cómo se define las urls de las oplicaciones
````
from django.urls import path 
from . import views


urlpatterns = [
    path('register/', views.register, name='register'),
    path('login/', views.login, name='login'),
    path('logout/', views.logout, name='logout')
]

````
