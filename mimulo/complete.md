# Technický popis pro nasazení měření na weby mimulo a kojeneckekojenecke-obleceni


Na webech už je nasazeno měření Zobrazení detailu produktu (*view_item*), Přidání do košíku (*add_to_cart*) a Dokončení objednávky (*purchase*), zde jsou uvedeny jen pro přehlednost.

## Nasazení měření elektronického obchodu

### Zobrazení výpisu produktů ([dokumentace](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm#view_item_list-gtm))
Na stránkách s výpisem produktů, přidat kód

```html
<script>
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'view_item_list',
  'ecommerce': {
    'items': [
      {
        'item_id': 'mr-w-002935-HP',
        'item_name': 'Playgo Chytání ryb do vany',
        'currency': 'CZK',
        'item_brand': 'PLAYGO',
        'item_category': 'Hračky',
        'item_category2': 'Do vody',
        'item_category3': 'Do vany',
        'price': 271.76
      },
      {
        'item_id': 'mr-w-001338-HP',
        'item_name': 'Flétna Krtek 33 cm',
        'currency': 'CZK',
        'item_brand': 'Wiky',
        'item_category': 'Hračky',
        'item_category2': 'Hudební',
        'price': 63.331
      },
      {
        ...
      }
    ]
  }
});
</script>
```

Pro každý produkt bude jeden objekt v poli `items`.


### Zobrazení detailu produktu ([dokumentace](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm#view_item-gtm))
Na stránkách s detailem produktu, přidat kód

```html
<script>
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'view_item',
  'ecommerce': {
    'items': [
      {
        'item_id': 'mr-w-002935-HP',
        'item_name': 'Playgo Chytání ryb do vany',
        'currency': 'CZK',
        'item_brand': 'PLAYGO',
        'item_category': 'Hračky',
        'item_category2': 'Do vody',
        'item_category3': 'Do vany',
        'price': 271.76
      },
      {
        ....
      }
    ]
  }
});
</script>
```

### Přidání do košíku ([dokumentace](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm#add_to_cart-gtm))
Po kliknutí na tlačítko "Přidat do košíku", případně "Do košíku" (při zobrazení hlášky *Zboží bylo vloženo do nákupního košíku*) vložit kód

```html
<script>
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'add_to_cart',
  'ecommerce': {
    'items': [
      {
        'item_id': 'mr-w-002935-HP',
        'item_name': 'Playgo Chytání ryb do vany',
        'currency': 'CZK',
        'item_brand': 'PLAYGO',
        'item_category': 'Hračky',
        'item_category2': 'Do vody',
        'item_category3': 'Do vany',
        'price': 271.76,
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

### Zobrazení košíku ([dokumentace](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm#view_cart-gtm))
Na stránce košíku (/ShoppingCart), vložit kód

```html
<script>
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'view_cart',
  'ecommerce': {
    currency: "CZK",
    value: 271.76,
    'items': [
      {
        'item_id': 'mr-w-002935-HP',
        'item_name': 'Playgo Chytání ryb do vany',
        'currency': 'CZK',
        'item_brand': 'PLAYGO',
        'item_category': 'Hračky',
        'item_category2': 'Do vody',
        'item_category3': 'Do vany',
        'price': 271.76,
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

### Zahájení nákupu ([dokumentace](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm#begin_checkout-gtm))
Na stránce objednávky (/Checkout), vložit kód

```html
<script>
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'begin_checkout',
  'ecommerce': {
    currency: "CZK",
    value: 271.76,
    'items': [
      {
        'item_id': 'mr-w-002935-HP',
        'item_name': 'Playgo Chytání ryb do vany',
        'currency': 'CZK',
        'item_brand': 'PLAYGO',
        'item_category': 'Hračky',
        'item_category2': 'Do vody',
        'item_category3': 'Do vany',
        'price': 271.76,
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

### Zadání platebních údajů ([dokumentace](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm#add_payment_info-gtm))
Na stránce objednávky (/Checkout), po výběru způsobu platby, vložit kód

```html
<script>
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'add_payment_info',
  'ecommerce': {
    currency: "CZK",
    value: 271.76,
    'items': [
      {
        'item_id': 'mr-w-002935-HP',
        'item_name': 'Playgo Chytání ryb do vany',
        'currency': 'CZK',
        'item_brand': 'PLAYGO',
        'item_category': 'Hračky',
        'item_category2': 'Do vody',
        'item_category3': 'Do vany',
        'price': 271.76,
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
    'transaction_id': 'MCZ24001056',
    'value': 361.85,
    'tax': 76.16,
    'shipping': 57.03,
    'currency': 'CZK',
    'coupon': 'SLEVA0',
    'items': [
      {
        'item_id': 'mr-w-002935-HP',
        'item_name': 'Playgo Chytání ryb do vany',
        'currency': 'CZK',
        'item_brand': 'PLAYGO',
        'item_category': 'Hračky',
        'item_category2': 'Do vody',
        'item_category3': 'Do vany',
        'price': 271.76,
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

Proměnná `value` by správně měla obsahovat konečnou cenu objednávky včetně dopravy a daně, které jsou samostatně vyčíslené v proměnných `tax` a `shipping`. Nyní to tak ale není a v rámci zachování porovnatelných čísel bych to nechal tak, jak to je.

### Další zdroje

* [Measure ecommerce - Developer Guide](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm)
* [[GA4] Dimensions and metrics](https://support.google.com/analytics/answer/9143382#dimensions&zippy=%2Cecommerce)
