# Technický popis pro nasazení měření na weby mimulo.(cz,sk,pl,hu,ro) a kojeneckekojenecke-obleceni.eu


Na webech už je nasazeno měření Zobrazení detailu produktu (*view_item*), Přidání do košíku (*add_to_cart*) a Dokončení objednávky (*purchase*), proto nejsou obsaženy v tomto přehledu, jdou zde jen kódy, které je potřeba přidat.

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

Pro každý produkt v objednávce bude jeden objekt v poli `items`.


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


### Další zdroje

* [Measure ecommerce - Developer Guide](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm)
* [[GA4] Dimensions and metrics](https://support.google.com/analytics/answer/9143382#dimensions&zippy=%2Cecommerce)
