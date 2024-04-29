> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/como-gestionar-ficheros-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Verificar si un archivo existe
```javascript
import { access } from 'node:fs';

access('archivo.txt', (err) => {
  if (err) {
    console.error('El archivo no existe');
    return;
  }
  
  console.log('El archivo existe');
});
```


## Copiar un archivo
```javascript
import { copyFile } from 'node:fs';

copyFile('origen.txt', 'destino.txt', (err) => {
  if (err) throw err;
  
  console.log('Archivo copiado exitosamente');
});
```


## Mover un archivo
```javascript
import { rename } from 'node:fs';

rename('antiguo.txt', 'nuevo.txt', (err) => {
  if (err) throw err;
  
  console.log('Archivo movido exitosamente');
});
```


## Borrar un archivo
```javascript
import { unlink } from 'node:fs';

unlink('archivo.txt', (err) => {
  if (err) throw err;
  
  console.log('Archivo borrado exitosamente');
});
```


## Lectura de archivo de texto
```
Este es un archivo de ejemplo.
Contiene algunas líneas de texto.
```

```javascript
import { readFile } from 'node:fs';

fs.readFile('datos.txt', 'utf8', (err, data) => {
  if (err) {
    console.error('Error al leer el archivo:', err);
    return;
  }
  
  console.log('Contenido del archivo:');
  console.log(data);
});
```


## Lectura de archivo de binario
```javascript
import { readFile } from 'node:fs';

fs.readFile('datos.txt',(err, data) => {
  if (err) {
    console.error('Error al leer el archivo:', err);
    return;
  }
  
  console.log('Contenido del archivo:');
  console.log(data);
});
```


## Añadir una línea a un archivo
```javascript
import { appendFile } from 'node:fs';

const nuevaLinea = 'Nueva línea a añadir';

appendFile('archivo.txt', `${nuevaLinea}\n`, (err) => {
  if (err) throw err;
  
  console.log('Línea añadida al archivo');
});
```


## Crear un nuevo archivo y escribir en él
```javascript
import { writeFile } from 'node:fs';

const contenido = 'Contenido del nuevo archivo';

writeFile('nuevo.txt', contenido, (err) => {
  if (err) throw err;
  
  console.log('Nuevo archivo creado y contenido escrito');
});
```


