# Cómo hacer un link
```
<p class="text-center mt-4">Ya tienes cuenta? <a href="{% url 'login' %}">Entrar</a></p>
```

# Cómo heredamos una plantilla
```
{% extends 'base.html' %}
{% load static %}

{%  block content %}
{% endblock %}
```

# Cómo hacemos un ciclo for
```
<ul class="list-menu">
  {% for category in links %}
      <li><a href="{{ category.get_url }}">{{ category.category_name }} </a></li>
  {% endfor %}
</ul>
```

# Cómo hacemos un IF ELSE
```
{% if cart_item.product.images %}
  <div class="aside"><img src="{{ cart_item.product.images.url }}" class="img-sm"></div>
{% else %}
   <div class="aside"><img src="{% static 'images/no_imagen_product.png' %}" class="img-sm"></div>
{% endif %}
```
