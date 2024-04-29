> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/como-hacer-test-unitarios-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Escribir Pruebas Unitarias
```javascript
// tests.mjs
import assert from 'node:assert';
import test from 'node:test';

test('that 1 is equal 1', () => {
  assert.strictEqual(1, 1);
});

test('that throws as 1 is not equal 2', () => {
  // throws an exception because 1 != 2
  assert.strictEqual(1, 2);
});
```


## Ejecutar las Pruebas
```bash
node tests.mjs
```


## Ejemplos adicionales de pruebas unitarias
```javascript
test('Comprobando que true es verdadero', () => {
  assert.strictEqual(true, true);
});

test('Comprobando que false es falso', () => {
  assert.strictEqual(false, false);
});

test('Comprobando que 0 es falsy', () => {
  assert.strictEqual(0, false);
});

test('Comprobando que "hello" es una cadena', () => {
  assert.strictEqual(typeof "hello", 'string');
});

test('Comprobando que [1, 2, 3] contiene el número 2', () => {
  assert.deepStrictEqual([1, 2, 3].includes(2), true);
});

test('Comprobando que {a: 1, b: 2} tiene la propiedad "a"', () => {
  assert.strictEqual(Object.prototype.hasOwnProperty.call({a: 1, b: 2}, 'a'), true);
});

test('Comprobando que una función suma dos números correctamente', () => {
  function add(a, b) {
    return a + b;
  }
  assert.strictEqual(add(2, 3), 5);
});
```


