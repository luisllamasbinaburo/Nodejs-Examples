> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/obtener-informacion-sistema-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Obtener información sobre el sistema
```javascript
import os from 'node:os';

console.log('Plataforma:', os.platform());
console.log('Arquitectura:', os.arch());
console.log('Versión del SO:', os.version());
console.log('Memoria total (bytes):', os.totalmem());
console.log('Memoria libre (bytes):', os.freemem());
console.log('Directorio temporal:', os.tmpdir());
console.log('Nombre del host:', os.hostname());
console.log('CPU:', os.cpus());
```


## Obtener información sobre los usuarios del sistema
```javascript
import os from 'node:os';

console.log('Información de usuario actual:', os.userInfo());
console.log('Directorio de inicio del usuario actual:', os.homedir());
```


## Obtener información sobre interfaces de red
```javascript
import os from 'node:os';

const interfaces = os.networkInterfaces();
console.log('Interfaces de red:', interfaces);
```


## Obtener información sobre el tiempo de actividad del sistema
```javascript
import os from 'node:os';

console.log('Tiempo de actividad del sistema (segundos):', os.uptime());
```


## Obtener información sobre las constantes del sistema
```javascript
import os from 'node:os';

console.log('Fin de línea predeterminado:', os.EOL);
console.log('Directorio de ejecución del proceso Node:', os.homedir());
console.log('Directorio temporal predeterminado:', os.tmpdir());
```


