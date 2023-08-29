# Technický popis pro nasazení měření na lauracoffee.cz
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
