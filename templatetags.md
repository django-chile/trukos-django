# Creamos una carpeta en la app llamada : templatetags
# Ponemos 
````
# __init__.py
# poll_extra.py

from django import template
from store.models import Product
register = template.Library()


@register.filter(name='get_listprice')
def get_listprice(product, arg):
    return Product.get_list_price(product, arg)
````

