> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/obtener-informacion-proceso-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Obtener argumentos de la línea de comandos
```javascript
import process from 'node:process';

const args = process.argv.slice(2);
console.log('Argumentos de la línea de comandos:', args);
```


## Obtener el directorio de trabajo actual
```javascript
import process from 'node:process';

const cwd = process.cwd();
console.log('Directorio de trabajo actual:', cwd);
```


## Salir del proceso con un código de salida
```javascript
import process from 'node:process';

// Salir con código de salida 0 (éxito)
process.exit(0);

// Salir con código de salida 1 (error)
process.exit(1);
```


## Obtener información sobre el entorno del proceso
```javascript
import process from 'node:process';

console.log('ID del proceso:', process.pid);
console.log('Versión de Node.js:', process.version);
console.log('Plataforma:', process.platform);
console.log('Arquitectura:', process.arch);
console.log('Variables de entorno:', process.env);
```


## Escuchar eventos del proceso
```javascript
import process from 'node:process';

process.on('exit', (code) => {
  console.log(`Proceso terminado con código de salida: ${code}`);
});

process.on('uncaughtException', (err) => {
  console.error('Excepción no capturada:', err);
});

process.on('SIGINT', () => {
  console.log('Se recibió la señal SIGINT (Ctrl+C)');
  process.exit(0);
});
```


## Cambiar el título de la ventana del proceso
```javascript
import process from 'node:process';

process.title = 'Mi Aplicación';
console.log('Título del proceso:', process.title);
```


## Lanzar un proceso
```javascript
import { spawn } from 'node:child_process';

// Comando para abrir gedit en Linux o macOS
const comando = 'gedit';

// Argumentos opcionales, en este caso no es necesario
const args = [];

const proceso = spawn(comando, args);

proceso.on('error', (err) => {
  console.error('Error al iniciar el proceso:', err);
});

proceso.on('exit', (code) => {
  console.log(`Proceso finalizado con código de salida: ${code}`);
});
```


