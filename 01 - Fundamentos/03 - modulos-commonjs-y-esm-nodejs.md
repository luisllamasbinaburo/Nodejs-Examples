> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/modulos-commonjs-y-esm-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## CommonJS :span[Legacy]{.label .yellow}
```javascript
// Importar un módulo
  const otroModulo = require('./otroModulo');

  // Exportar un módulo
  module.exports = {
    foo: 'bar'
  };
```


## ECMAScript Modules (ESM) :span[Standard]{.label .green}
```javascript
// Importar un módulo
  import otroModulo from './otroModulo';

  // Exportar un módulo
  export const foo = 'bar';
```


## Cómo usar módulos CommonJS en ESM
```javascript
import { createRequire } from 'node:module';
const require = createRequire(import.meta.url);

const tus_funciones = require('tu_modulo_commonjs');
```


