> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/como-usar-sqlite-con-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Cómo conectar Node.js a SQLite
```bash
npm install sqlite3
```


## Configuración de una DB en memoria
```javascript
import sqlite from 'sqlite3';

// Crear una conexión a una base de datos en memoria
const db = new sqlite.Database(':memory:');

// Operaciones con la base de datos
db.serialize(() => {
    // Crear una tabla
    db.run("CREATE TABLE lorem (info TEXT)");

    // Insertar datos en la tabla
    const stmt = db.prepare("INSERT INTO lorem VALUES (?)");
    for (let i = 0; i < 10; i++) {
        stmt.run("Ipsum " + i);
    }
    stmt.finalize();

    // Consultar datos de la tabla
    db.each("SELECT rowid AS id, info FROM lorem", (err, row) => {
        console.log(row.id + ": " + row.info);
    });
});

// Cerrar la conexión cuando hayas terminado
db.close();
```


## Creación de una DB en un archivo
```javascript
import sqlite from 'sqlite3';
const dbPath = './database.db'; // Ruta al archivo de base de datos

// Conectar a la base de datos en un archivo físico
const db = new sqlite.Database(dbPath);

// El resto del código es similar al ejemplo anterior
// ...
```


## Creación de Datos
```javascript
async function insertData(name, email) {
  try {
    // Insertamos datos en la tabla users
    await db.run("INSERT INTO users (name, email) VALUES (?, ?)", [name, email]);
    console.log('Datos insertados exitosamente');
  } catch (error) {
    console.error('Error al insertar datos:', error);
  }
}

insertData('John Doe', 'john@example.com'); // Ejecutamos la función insertData con los datos proporcionados
```


## Lectura de Datos
```javascript
async function fetchData() {
  try {
    // Consultamos todos los usuarios de la tabla users
    const users = await db.all("SELECT * FROM users");
    console.log('Todos los usuarios:', users);
  } catch (error) {
    console.error('Error al obtener datos:', error);
  }
}

fetchData(); // Ejecutamos la función fetchData para obtener todos los usuarios
```


## Actualización de Datos
```javascript
async function updateData(userId, newName) {
  try {
    // Actualizamos el nombre del usuario con el userId especificado
    await db.run("UPDATE users SET name = ? WHERE id = ?", [newName, userId]);
    console.log('Datos actualizados exitosamente');
  } catch (error) {
    console.error('Error al actualizar datos:', error);
  }
}

updateData(1, 'Jane Smith'); // Ejecutamos la función updateData con los datos proporcionados
```


## Eliminación de Datos
```javascript
async function deleteData(userId) {
  try {
    // Eliminamos el usuario con el userId especificado
    await db.run("DELETE FROM users WHERE id = ?", [userId]);
    console.log('Datos eliminados exitosamente');
  } catch (error) {
    console.error('Error al eliminar datos:', error);
  }
}

deleteData(2); // Ejecutamos la función deleteData con el ID del usuario a eliminar
```


