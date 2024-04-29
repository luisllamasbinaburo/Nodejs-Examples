> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/como-usar-mysql-con-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Cómo conectar Node.js a MySQL
```bash
npm install mysql2
```


## Creación del archivo de conexión a la base de datos
```javascript
import mysql from 'mysql2/promise';

async function connect() {
  try {
    const connection = await mysql.createConnection({
      host: 'localhost',
      user: 'tu_usuario',
      password: 'tu_contraseña',
      database: 'nombre_de_tu_db',
    });
    console.log('Conexión a MySQL establecida.');
    return connection;
  } catch (error) {
    console.error('Error al conectar a MySQL:', error);
    throw error;
  }
}

export default connect;
```


## Creando la conexión a la base de datos
```javascript
import connect from './dbConnection.mjs';

async function fetchData() {
  const db = await connect();
  try {
    // Consulta para obtener todos los usuarios
    const [rows, fields] = await db.execute('SELECT * FROM users');
    console.log('Todos los usuarios:', rows);

    // Consulta para obtener usuarios por ciudad
    const city = 'New York';
    const [cityRows, cityFields] = await db.execute('SELECT * FROM users WHERE city = ?', [city]);
    
    console.log(`Usuarios en ${city}:`, cityRows);
  } catch (error) {
    console.error('Error al obtener datos:', error);
  } finally {
    db.end();
  }
}

fetchData();
```


## Creación de Datos
```javascript
async function insertData(name, email) {
  // Establecemos la conexión a la base de datos
  const db = await connect(); 
  try {
    // Ejecutamos la consulta SQL para insertar datos
    const [result] = await db.execute('INSERT INTO users (name, email) VALUES (?, ?)', [name, email]); 
    // Mostramos el resultado de la operación
    console.log('Datos insertados:', result); 
  } catch (error) {
    // Manejamos cualquier error que ocurra durante la inserción de datos
    console.error('Error al insertar datos:', error); 
  } finally {
    // Cerramos la conexión a la base de datos, independientemente del resultado
    db.end(); 
  }
}

insertData('John Doe', 'john@example.com'); // Ejecutamos la función insertData con los datos proporcionados
```


## Lectura de Datos
```javascript
async function fetchData() {
  // Establecemos la conexión a la base de datos
  const db = await connect(); 
  try {
    // Ejecutamos la consulta SQL para obtener todos los usuarios
    const [rows, fields] = await db.execute('SELECT * FROM users'); 
    // Mostramos todos los usuarios recuperados de la base de datos
    console.log('Todos los usuarios:', rows); 
  } catch (error) {
    // Manejamos cualquier error que ocurra durante la lectura de datos
    console.error('Error al obtener datos:', error); 
  } finally {
    // Cerramos la conexión a la base de datos, independientemente del resultado
    db.end(); 
  }
}

fetchData(); // Ejecutamos la función fetchData para obtener todos los usuarios
```


## Actualización de Datos
```javascript
async function updateData(userId, newName) {
  // Establecemos la conexión a la base de datos
  const db = await connect(); 
  try {
    // Ejecutamos la consulta SQL para actualizar datos
    const [result] = await db.execute('UPDATE users SET name = ? WHERE id = ?', [newName, userId]); 
    // Mostramos el resultado de la operación
    console.log('Datos actualizados:', result); 
  } catch (error) {
    // Manejamos cualquier error que ocurra durante la actualización de datos
    console.error('Error al actualizar datos:', error); 
  } finally {
    // Cerramos la conexión a la base de datos, independientemente del resultado
    db.end(); 
  }
}

updateData(1, 'Jane Smith'); // Ejecutamos la función updateData con los datos proporcionados
```


## Eliminación de Datos
```javascript
async function deleteData(userId) {
  // Establecemos la conexión a la base de datos
  const db = await connect(); 
  try {
    // Ejecutamos la consulta SQL para eliminar datos
    const [result] = await db.execute('DELETE FROM users WHERE id = ?', [userId]); 
    // Mostramos el resultado de la operación
    console.log('Datos eliminados:', result); 
  } catch (error) {
    // Manejamos cualquier error que ocurra durante la eliminación de datos
    console.error('Error al eliminar datos:', error); 
  } finally {
    // Cerramos la conexión a la base de datos, independientemente del resultado
    db.end(); 
  }
}

deleteData(2); // Ejecutamos la función deleteData con el ID del usuario a eliminar
```


