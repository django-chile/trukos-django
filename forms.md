# Cómo se trabaja en la plantilla
````
{% extends 'base.html' %}
{% load static %}

{%  block content %}

<!-- ========================= SECTION CONTENT ========================= -->
<section class="section-content padding-y">

    <!-- ============================ COMPONENT REGISTER   ================================= -->
        <div class="card mx-auto" style="max-width:520px; margin-top:40px;">
          <article class="card-body">
            {%  include 'includes/alerts.html' %}
            

            <header class="mb-4"><h4 class="card-title">Registrarse</h4></header>
            <form action="{% url 'register' %}" method="POST">
                {% csrf_token %}

                {% comment %} {{ form.as_p }} {% endcomment %}

                    <div class="form-row">
                        <div class="col form-group">
                            <label>Nombre</label>
                            {{form.first_name}}
                        </div> <!-- form-group end.// -->
                        <div class="col form-group">
                            <label>Apellidos</label>
                            {{form.last_name}}
                        </div> <!-- form-group end.// -->
                    </div> <!-- form-row end.// -->

                    <div class="form-row">
                        <div class="col form-group">
                            <label>Número Telefónico</label>
                            {{form.phone_number}}
                        </div> <!-- form-group end.// -->
                        <div class="col form-group">
                            <label>Email</label>
                            {{form.email}}
                        </div> <!-- form-group end.// -->
                    </div> <!-- form-row end.// -->

                    <div class="form-row">
                        <div class="form-group col-md-6">
                            <label>Crear Contraseña</label>
                            {{form.password}}
                        </div> <!-- form-group end.// --> 
                        <div class="form-group col-md-6">
                            <label>Repetir Contraseña</label>
                            {{form.confirm_password}}
                        </div> <!-- form-group end.// -->  
                    </div>
                    <div class="form-group">
                        <button type="submit" class="btn btn-primary btn-block"> Registrarse  </button>
                    </div> <!-- form-group// --> 
                    
                    {{ form.email.errors }}
                    {{ form.non_field_errors }}
                        
                </form>
            </article><!-- card-body.// -->
        </div> <!-- card .// -->
        <p class="text-center mt-4">Ya tienes cuenta? <a href="{% url 'login' %}">Entrar</a></p>
        <br><br>
    <!-- ============================ COMPONENT REGISTER  END.// ================================= -->
    
    
    </section>
    <!-- ========================= SECTION CONTENT END// ========================= -->

{% endblock %}
````

# Como se trabaja en la vista
````
from django.shortcuts import render, redirect
from accounts.forms import RegistrationForm
from accounts.models import Account
from django.contrib import messages
# Create your views here.

def register(request):
    form = RegistrationForm
    if request.method == 'POST':
        form = RegistrationForm(request.POST)
        if form.is_valid():
            first_name = form.cleaned_data['first_name']
            last_name = form.cleaned_data['last_name']
            phone_number = form.cleaned_data['phone_number']
            email = form.cleaned_data['email']
            password = form.cleaned_data['password']
            username = email.split('@')[0]
            
            # Creamos una instancia de usuario
            user = Account.objects.create_user(first_name=first_name, last_name=last_name, email=email, username=username, password=password)
            user.phone_number = phone_number
            user.save()
            messages.success(request, 'Se registro el usuario exitosamente')
            return redirect('register')
            
    context = {
        'form' : form
    }
    return render(request, 'accounts/register.html', context)
````

# Ejemplo de forms
````
````
from dataclasses import field
from distutils.command.clean import clean
from django import forms
from .models import Account

class RegistrationForm(forms.ModelForm):
    password = forms.CharField(widget=forms.PasswordInput(attrs={
        'placeholder' : 'Ingrese Contraseña',
        'class' : 'form-control'
    }))
    
    confirm_password = forms.CharField(widget=forms.PasswordInput(attrs={
        'placeholder' : 'Confirmar Contraseña',
        'class' : 'form-control'
    }))
    
    class Meta:
        model = Account
        fields = ['first_name', 'last_name', 'phone_number', 'email', 'password']
        
    
    def __init__(self, *arg, **kwargs):
        super(RegistrationForm, self).__init__(*arg, **kwargs)
        self.fields['first_name'].widget.attrs['placeholder'] = 'Nombre'
        self.fields['last_name'].widget.attrs['placeholder'] = 'Apellido'
        self.fields['phone_number'].widget.attrs['placeholder'] = 'Número de teléfono'
        self.fields['email'].widget.attrs['placeholder'] = 'Email'
        
        for field in self.fields:
            self.fields[field].widget.attrs['class']='form-control'
            
            
    def clean(self):
        cleaned_data = super(RegistrationForm, self).clean()
        password = cleaned_data.get('password')
        confirm_password = cleaned_data.get('confirm_password')
        
        if password != confirm_password:
            raise forms.ValidationError(
                "El password no coincide"
            )
