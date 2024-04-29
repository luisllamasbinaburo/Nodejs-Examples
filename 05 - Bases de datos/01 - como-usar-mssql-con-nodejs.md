> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/como-usar-mssql-con-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Cómo conectar Node.js a MSSQL
```bash
npm install mssql
```


## Configuración de la Conexión
```javascript
const dbConfig = {
  user: 'tu_usuario',
  password: 'tu_password',
  server: 'localhost',  // Puede ser una dirección IP o nombre del servidor
  port: 1433,
  database: 'nombre_de_tu_base_de_datos',
  dialect: "mssql",
  options: {
    encrypt: false,
    trustServerCertificate: true,
    trustedConnection: true,  
  },
};
```


## Estableciendo la Conexión
```javascript
import sql from 'mssql';

import dbConfig from './dbConfig.mjs';

// Función para conectarse y realizar una consulta
async function conectarYConsultar() {
  try {
    // Conectarse a la base de datos
    await sql.connect(config);

    // Consulta SQL
    const result = await sql.query`SELECT * FROM TuTabla`;

    // Imprimir resultados
    console.dir(result);

  } catch (err) {
    // Manejar errores
    console.error('Error al intentar conectarse:', err);
  } finally {
    // Cerrar la conexión al finalizar
    sql.close();
  }
}

// Llamar a la función para conectar y consultar
conectarYConsultar();
```


## Trusted connection
```bash
npm install msnodesqlv8
```

```javascript
const sql = require('mssql/msnodesqlv8');

var dbConfig = {
  server: 'localhost',
  port: 1433,
  database: 'curso',
  driver: "msnodesqlv8",
  options: {
    trustedConnection: true,    
  }
}
```

```javascript
import { createRequire } from 'node:module';
const require = createRequire(import.meta.url);
const sql = require('mssql/msnodesqlv8');

import dbConfig from './dbconnection.mjs';

async function conectarYConsultar() {
    try {
      // resto del contenido
      ///...
}
```


## Consulta Simple
```javascript
async function consultarDatos() {
  try {
    const result = await sql.query`SELECT * FROM TuTabla`;
    console.dir(result);
  } catch (error) {
    console.error('Error al ejecutar la consulta:', error);
  }
}
```


## Consulta Parametrizada
```javascript
async function consultaParametrizada() {
  try {
    const nombre = 'John';
    const result = await sql.query`SELECT * FROM TuTabla WHERE Nombre = ${nombre}`;
    console.dir(result);
  } catch (error) {
    console.error('Error al ejecutar la consulta parametrizada:', error);
  }
}
```


## Transacciones
```javascript
async function ejecutarTransaccion() {
  try {
    await sql.connect(config);
    const transaction = new sql.Transaction();
    await transaction.begin();

    const result1 = await transaction.request().query('INSERT INTO TuTabla (campo1, campo2) VALUES (valor1, valor2)');
    const result2 = await transaction.request().query('UPDATE OtraTabla SET campo = nuevo_valor WHERE condicion');

    await transaction.commit();
    console.log('Transacción completada.');
  } catch (error) {
    console.error('Error al ejecutar la transacción:', error);
    await transaction.rollback();
  } finally {
    sql.close();
  }
}
```


