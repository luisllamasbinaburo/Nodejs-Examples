> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/como-manejar-path-ficheros-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Unir rutas
```javascript
import path from 'node:path';

const ruta1 = '/carpeta1';
const ruta2 = 'subcarpeta/archivo.txt';

const rutaCompleta = path.join(ruta1, ruta2);
console.log('Ruta completa:', rutaCompleta);
```


## Normalizar una ruta
```javascript
import path from 'node:path';

const ruta = '/carpeta1//subcarpeta/./archivo.txt';
const rutaNormalizada = path.normalize(ruta);

console.log('Ruta normalizada:', rutaNormalizada);
// Ruta normalizada: \carpeta1\subcarpeta\archivo.txt
```


## Obtener el nombre de un archivo
```javascript
import path from 'node:path';

const ruta = '/carpeta1/subcarpeta/archivo.txt';
const nombreBase = path.basename(ruta);

console.log('Nombre del archivo:', nombreBase);
//Nombre del archivo: archivo.txt
```


## Obtener el nombre del directorio
```javascript
import path from 'node:path';

const ruta = '/carpeta1/subcarpeta/archivo.txt';
const nombreDirectorio = path.dirname(ruta);

console.log('Nombre del directorio:', nombreDirectorio);
//Nombre del directorio: /carpeta1/subcarpeta
```


## Obtener la extensión de un archivo
```javascript
import path from 'node:path';

const ruta = '/carpeta1/subcarpeta/archivo.txt';
const extension = path.extname(ruta);

console.log('Extensión del archivo:', extension);
// Extensión del archivo: .txt
```


## Convertir una ruta relativa en absoluta
```javascript
import path from 'node:path';

const rutaRelativa = '../carpeta1/subcarpeta/archivo.txt';
const rutaAbsoluta = path.resolve(rutaRelativa);

console.log('Ruta absoluta:', rutaAbsoluta);
// Ruta absoluta: C:\..lo_que_sea..\carpeta1\subcarpeta\archivo.txt
```


