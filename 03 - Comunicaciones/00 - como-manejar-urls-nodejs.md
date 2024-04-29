> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/como-manejar-urls-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Parseo de una URL
```javascript
import { URL } from 'node:url';

const urlTexto = 'https://www.ejemplo.com/ruta/subruta?param1=valor1&param2=valor2';
const miUrl = new URL(urlTexto);

console.log('Protocolo:', miUrl.protocol);
console.log('Host:', miUrl.host);
console.log('Ruta:', miUrl.pathname);
console.log('Parámetros de búsqueda:', miUrl.searchParams);
```


## Construcción de una URL
```javascript
import { URL } from 'node:url';

const baseUrl = 'https://www.ejemplo.com';
const ruta = '/ruta/subruta';
const params = new URLSearchParams({
  param1: 'valor1',
  param2: 'valor2'
});

const urlCompleta = new URL(ruta, baseUrl);
urlCompleta.search = params.toString();

console.log('URL Completa:', urlCompleta.href);
```


## Modificación de parámetros de una URL
```javascript
import { URLSearchParams } from 'node:url';

const url = new URL('https://www.ejemplo.com/?param1=valor1&param2=valor2');

// Obtener parámetros
console.log('Parámetro 1:', url.searchParams.get('param1'));
console.log('Parámetro 2:', url.searchParams.get('param2'));

// Añadir parámetro
url.searchParams.append('param3', 'valor3');
console.log('URL con nuevo parámetro:', url.href);

// Eliminar parámetro
url.searchParams.delete('param2');
console.log('URL sin param2:', url.href);
```


## Resolución de URLs relativas
```javascript
import { resolve } from 'node:path';

const baseUrl = 'https://www.ejemplo.com/carpeta1/';
const urlRelativa = 'subcarpeta/archivo.html';

const urlResuelta = new URL(urlRelativa, baseUrl);
console.log('URL Resuelta:', urlResuelta.href);
```


## Verificación de la validez de una URL
```javascript
import { URL } from 'node:url';

function esURLValida(url) {
  try {
    new URL(url);
    return true;
  } catch (error) {
    return false;
  }
}

console.log('¿Es válida la URL?', esURLValida('https://www.ejemplo.com')); // true
console.log('¿Es válida la URL?', esURLValida('esto no es una URL')); // false
```


