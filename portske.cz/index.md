# Technický popis pro nasazení měření na portske.cz



## Měření interakcí na webu
### Měření registrace
Po úspěšné registraci vložit kód

```html
<script>
dataLayer.push({'event': 'sign_up'});
</script>
```

### Měření přihlášení
Po úspěšném přihlášení vložit kód

```html
<script>
dataLayer.push({'event': 'login'});
</script>
```

## Nasazení měření elektronického obchodu

### Zobrazení detailu produktu ([dokumentace](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm#view_item_details))
Na stránkách s detailem produktu, přidat kód

```html
<script>
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'view_item',
  'ecommerce': {
    'items': [
      {
        'item_id': 'ZV21050',
        'item_name': 'Quinta do Noval Black',
        'currency': 'CZK',
        'item_brand': 'Quinta do Noval',
        'item_category': 'PORTSKÉ VÍNO',
        'item_category2': 'Portské víno reservy',
        'price': 580
      },
      {
        .... 
      }
    ]
  }
});
</script>
```

### Přidání do košíku ([dokumentace](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm#add_or_remove_an_item_from_a_shopping_cart))
Po kliknutí na tlačítko “Vložit do košíku”, případně "Do košíku" (při zobrazení hlášky *Produkt byl vložen do košíku*) vložit kód

```html
<script>
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'add_to_cart',
  'ecommerce': {
    'items': [
      {
        'item_id': 'ZV21050',
        'item_name': 'Quinta do Noval Black',
        'currency': 'CZK',
        'item_brand': 'Quinta do Noval',
        'item_category': 'PORTSKÉ VÍNO',
        'item_category2': 'Portské víno reservy',
        'price': 580,
        'quantity': 1  
      },
      {
        .... 
      }
    ]
  }
});
</script>
```

### Zobrazení košíku ([dokumentace](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm#initiate_the_checkout_process))
Na stránce košíku (/kosik), vložit kód

```html
<script>
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'begin_checkout',
  'ecommerce': {    
    'items': [
      {
        'item_id': 'ZV21050',
        'item_name': 'Quinta do Noval Black',
        'currency': 'CZK',
        'item_brand': 'Quinta do Noval',
        'item_category': 'PORTSKÉ VÍNO',
        'item_category2': 'Portské víno reservy',
        'price': 580,
        'quantity': 1
      },
      {
        ....
      }
    ]
  }
});
</script>
```
Pro každý produkt v objednávce bude jeden objekt v poli `items`.

### Dokončení objednávky ([dokumentace](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm#purchase))
Po dokončení objednávky, na děkovací stránce, vložit kód

```html
<script>
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'purchase',
  'ecommerce': {
    'transaction_id': 'T12345',
    'value': 580,
    'tax': 100.66,
    'shipping': 0,
    'currency': 'CZK',
    'coupon': 'SLEVA20',
    'items': [
      {
        'item_id': 'ZV21050',
        'item_name': 'Quinta do Noval Black',
        'currency': 'CZK',
        'item_brand': 'Quinta do Noval',
        'item_category': 'PORTSKÉ VÍNO',
        'item_category2': 'Portské víno reservy',
        'price': 580,
        'quantity': 1
      },
      {
        ....
      }
    ]
  }
});
</script>
```
Pro každý produkt v objednávce bude jeden objekt v poli `items`. 

### Další zdroje

* [Measure ecommerce - Developer Guide](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm)
* [[GA4] Dimensions and metrics](https://support.google.com/analytics/answer/9143382#dimensions&zippy=%2Cecommerce)
