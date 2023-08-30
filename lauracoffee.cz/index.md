# Technický popis pro nasazení měření na lauracoffee.cz

## Odstranění kódu Google Analytics
Měření do Google Analytics bude nově probíhat přes GTM, proto je potřeba ze všech stránek původní měřící kód odstranit.

## Nasazení Google Tag Manageru
Nasazení probíhá vložením kódu GTM kontejneru na všechny stránky webu. Co nejvýše v sekci head, co nejblíže k značce `<head>`, je potřeba vložit kód:

```html
<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-TQFZ3WSF');</script>
<!-- End Google Tag Manager -->
```

a na začátek sekce body, těsně za značku <body>, je potřeba vložit kód:

```html
<!-- Google Tag Manager (noscript) -->
<noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-TQFZ3WSF"
height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
<!-- End Google Tag Manager (noscript) -->
```

Více informací o nasazení GTM lze najít v [dokumentaci](https://developers.google.com/tag-manager/quickstart).

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

### Zobrazení seznamu produktů ([dokumentace](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm#select_an_item_from_a_list))
Na stránkách s výpisem produktů, přidat kód

```html
<script>
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'view_item_list',
  'ecommerce': {
    'items': [
      {
        'item_id': '123',
        'item_name': 'Káva Laura',
        'currency': 'CZK',
        'item_brand': 'lauracoffee',
        'item_category': 'Káva',        
        'price': 220
      },
      {
        .... 
      }
    ]
  }
});
</script>
```

Pro každý zobrazený produkt bude jeden objekt v poli `items`.

### Zobrazení detailu produktu ([dokumentace](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce?client_type=gtm#view_item))
Na stránkách s detailem produktu, přidat kód

```html
<script>
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'view_item',
  'ecommerce': {
    'items': [
      {
        'item_id': '123',
        'item_name': 'Káva Laura',
        'currency': 'CZK',
        'item_brand': 'lauracoffee',
        'item_category': 'Káva',        
        'price': 220
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
Po kliknutí na tlačítko “Vložit do košíku”, případně "hodit do košíku" vložit kód

```html
<script>
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'add_to_cart',
  'ecommerce': {
    'items': [
      {
        'item_id': '123',
        'item_name': 'Káva Laura',
        'currency': 'CZK',
        'item_brand': 'lauracoffee',
        'item_category': 'Káva',        
        'item_variant': '250 g',
        'price': 220,
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
Na stránce košíku (/basket), vložit kód

```html
<script>
dataLayer.push({ ecommerce: null });
dataLayer.push({
  'event': 'begin_checkout',
  'ecommerce': {    
    'items': [
      {
        'item_id': '123',
        'item_name': 'Káva Laura',
        'currency': 'CZK',
        'item_brand': 'lauracoffee',
        'item_category': 'Káva',
        'item_variant': '250 g',
        'price': 220,
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
    'value': 220,
    'tax': 38.18,
    'shipping': 0,
    'currency': 'CZK',
    'coupon': 'SLEVA20',
    'items': [
      {
        'item_id': '123',
        'item_name': 'Káva Laura',
        'currency': 'CZK',
        'item_brand': 'lauracoffee',
        'item_category': 'Káva',
        'item_variant': '250 g',
        'price': 220,
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
