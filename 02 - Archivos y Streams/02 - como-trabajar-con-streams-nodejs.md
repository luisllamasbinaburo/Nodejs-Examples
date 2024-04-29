> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/como-trabajar-con-streams-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Leer un Archivo con Readable Streams
```javascript
import fs from 'node:fs';

const readableStream = fs.createReadStream('archivo.txt', 'utf8');

readableStream.on('data', (chunk) => {
  console.log('Datos recibidos:', chunk);
});

readableStream.on('end', () => {
  console.log('Lectura de archivo completa');
});

readableStream.on('error', (err) => {
  console.error('Error al leer el archivo:', err);
});
```


## Escribir en un Archivo con Writable Streams
```javascript
import fs from 'node:fs';

const writableStream = fs.createWriteStream('nuevoArchivo.txt', 'utf8');

writableStream.write('Esto es un texto que será escrito en el archivo.\n');
writableStream.write('Podemos escribir datos de forma incremental.\n');

writableStream.end('Finalizando escritura en el archivo.\n');

writableStream.on('finish', () => {
  console.log('Escritura de archivo completa');
});

writableStream.on('error', (err) => {
  console.error('Error al escribir en el archivo:', err);
});
```


## Piping (tubería) entre streams
```javascript
import { createReadStream, createWriteStream } from 'node:fs';

const readStream = createReadStream('archivo.txt');
const writeStream = createWriteStream('copiaArchivo.txt');

readStream.pipe(writeStream);

writeStream.on('finish', () => {
  console.log('Archivo copiado exitosamente.');
});

writeStream.on('error', (err) => {
  console.error('Error al copiar el archivo:', err);
});
```


## Combinar múltiples streams
```javascript
import { createReadStream, createWriteStream, Transform } from 'node:fs';

const readStream = createReadStream('archivo.txt', 'utf8');
const writeStream = createWriteStream('mayusculas.txt');

const transformStream = new Transform({
  transform(chunk, encoding, callback) {
    this.push(chunk.toString().toUpperCase());
    callback();
  }
});

readStream.pipe(transformStream).pipe(writeStream);

writeStream.on('finish', () => {
  console.log('Archivo transformado y escrito en mayúsculas.');
});

writeStream.on('error', (err) => {
  console.error('Error al transformar y escribir el archivo:', err);
});
```


