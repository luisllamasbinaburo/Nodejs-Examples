> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/funciones-temporales-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## setTimeout
```javascript
const delay = 3000; // 3 segundos

const timeoutId = setTimeout(() => {
  console.log('¡Han pasado 3 segundos!');
}, delay);

// Para cancelar el timeout antes de que se ejecute
// clearTimeout(timeoutId);
```


## setInterval
```javascript
const intervalo = 2000; // 2 segundos

const intervalId = setInterval(() => {
  console.log('¡Hola cada 2 segundos!');
}, intervalo);

// Para detener el intervalo después de cierto tiempo
/* setTimeout(() => {
  clearInterval(intervalId);
}, 10000); */ // Detener después de 10 segundos
```


## Ejemplo combinado de setTimeout y clearInterval
```javascript
let segundos = 0;

const intervalId = setInterval(() => {
  segundos++;
  console.log('Han pasado ' + segundos + ' segundos.');

  if (segundos === 5) {
    clearInterval(intervalId);
    console.log('El intervalo se detuvo después de 5 segundos.');
  }
}, 1000); // Cada segundo
```


## setImmediate
```javascript
setImmediate(() => {
  console.log('Esto se ejecuta en el siguiente ciclo de eventos.');
});
```


## process.nextTick
```javascript
process.nextTick(() => {
  console.log('Esto se ejecuta al final del ciclo actual.');
});
```


