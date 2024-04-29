> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/como-usar-modulos-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Creación de un módulo
```javascript
// Función para sumar dos números
export function sumar(a, b) {
 return a + b;
}

// Función para restar dos números
export function restar(a, b) {
 return a - b;
}
```


## Importación del módulo
```javascript
// Importar las funciones del módulo operaciones.mjs
import { sumar, restar } from './operaciones.mjs';

// Utilizar las funciones importadas
console.log(sumar(5, 3)); // Salida: 8
console.log(restar(10, 4)); // Salida: 6
```


## Exportación de variables
```javascript
// Exportar una variable
export let nombre = 'Juan';

// Exportar una constante
export const PI = 3.14159265359;
```

```javascript
import { nombre, PI } from './variables.mjs';

console.log(nombre); // Salida: Juan
console.log(PI); // Salida: 3.14159265359
```


## Ejecución del Programa
```bash
node app.js
```


