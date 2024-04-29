> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/como-usar-mongodb-con-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Cómo conectar Node.js a MongoDB
```bash
npm install mongodb
```


## Paso 2: Creación del Archivo de Conexión
```javascript
import { MongoClient } from 'mongodb';

const uri = 'mongodb://localhost:27017'; // URL de conexión a tu base de datos
const dbName = 'mydatabase'; // Nombre de tu base de datos

async function connect() {
  try {
    const client = new MongoClient(uri);
    await client.connect();
    const db = client.db(dbName);
    console.log('Conexión a MongoDB establecida.');
    return db;
  } catch (error) {
    console.error('Error al conectar a MongoDB:', error);
    throw error;
  }
}

export default connect;
```


## Uso de la Conexión en tu Aplicación
```javascript
import connect from './dbConnection.mjs';

async function fetchData() {
  const db = await connect();
  try {
    const collection = db.collection('mi_coleccion');
    const result = await collection.find({}).toArray();
    console.log('Documentos obtenidos:', result);
  } catch (error) {
    console.error('Error al obtener datos:', error);
  } finally {
    db.close();
  }
}

fetchData();
```


## Creación de Datos
```javascript
const MongoClient = require('mongodb').MongoClient;

const url = 'mongodb://localhost:27017';
const dbName = 'mi_base_de_datos';

MongoClient.connect(url, { useNewUrlParser: true, useUnifiedTopology: true }, (err, client) => {
  if (err) throw err;

  const db = client.db(dbName);
  const collection = db.collection('mi_coleccion');

  const documentoNuevo = { nombre: 'Ejemplo', edad: 30 };

  collection.insertOne(documentoNuevo, (err, result) => {
    if (err) throw err;
    console.log('Documento insertado correctamente');
    client.close();
  });
});
```


## Lectura de Datos
```javascript
const MongoClient = require('mongodb').MongoClient;

const url = 'mongodb://localhost:27017';
const dbName = 'mi_base_de_datos';

MongoClient.connect(url, { useNewUrlParser: true, useUnifiedTopology: true }, (err, client) => {
  if (err) throw err;

  const db = client.db(dbName);
  const collection = db.collection('mi_coleccion');

  collection.find({}).toArray((err, docs) => {
    if (err) throw err;
    console.log('Documentos encontrados:');
    console.log(docs);
    client.close();
  });
});
```


## Actualización de Datos
```javascript
const MongoClient = require('mongodb').MongoClient;

const url = 'mongodb://localhost:27017';
const dbName = 'mi_base_de_datos';

MongoClient.connect(url, { useNewUrlParser: true, useUnifiedTopology: true }, (err, client) => {
  if (err) throw err;

  const db = client.db(dbName);
  const collection = db.collection('mi_coleccion');

  const filtro = { nombre: 'Ejemplo' };
  const nuevoValor = { $set: { edad: 35 } };

  collection.updateOne(filtro, nuevoValor, (err, result) => {
    if (err) throw err;
    console.log('Documento actualizado correctamente');
    client.close();
  });
});
```


## Eliminación de Datos
```javascript
const MongoClient = require('mongodb').MongoClient;

const url = 'mongodb://localhost:27017';
const dbName = 'mi_base_de_datos';

MongoClient.connect(url, { useNewUrlParser: true, useUnifiedTopology: true }, (err, client) => {
  if (err) throw err;

  const db = client.db(dbName);
  const collection = db.collection('mi_coleccion');

  const filtro = { nombre: 'Ejemplo' };

  collection.deleteOne(filtro, (err, result) => {
    if (err) throw err;
    console.log('Documento eliminado correctamente');
    client.close();
  });
});
```


