> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/como-usar-sequalize-con-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Cómo conectar Node.js a SQLite
```bash
npm install sequelize
```

```bash
# instalar uno de los siguientes driver

npm install mysql2    # para mysql2 (MariaDB / MySQL)
npm install pg        # para pg (PostgreSQL)
npm install sqlite3   # para sqlite3 (SQLite)
npm install tedious   # para tedious (Microsoft SQL Server / Express SQL)
npm install oracledb  # para oracledb (Oracle Database)
```


## Configuración de la conexión a la base de datos
```javascript
const Sequelize = require('sequelize');

// Configuración de la conexión a la base de datos
const sequelize = new Sequelize('nombre_basedatos', 'usuario', 'contraseña', {
  host: 'localhost',
  dialect: 'mysql',
});
```


## Definición de un Modelo
```javascript
const Usuario = sequelize.define('usuario', {
  nombre: {
    type: Sequelize.STRING,
    allowNull: false,
  },
  edad: {
    type: Sequelize.INTEGER,
    allowNull: false,
  },
  correo: {
    type: Sequelize.STRING,
    allowNull: false,
    unique: true,
  },
});
```


## Sincronizar y utilizar el modelo
```javascript
(async () => {
  await sequelize.sync({ force: true }); // Sincronizar modelo con la base de datos
  
  // Crear un nuevo usuario
  const nuevoUsuario = await Usuario.create({
    nombre: 'Juan',
    edad: 25,
    correo: 'juan@example.com',
  });
  
  console.log('Usuario creado:', nuevoUsuario.toJSON());
  
  // Consultar usuarios
  const usuarios = await Usuario.findAll();
  console.log('Usuarios encontrados:', usuarios.map(u => u.toJSON()));
  
  // Actualizar usuario
  await Usuario.update({ edad: 30 }, { where: { nombre: 'Juan' } });
  
  // Eliminar usuario
  await Usuario.destroy({ where: { nombre: 'Juan' } });
})();
```


## Creación de Datos
```javascript
(async () => {
  await sequelize.sync({ force: true }); // Sincronizar modelo con la base de datos
  
  const nuevoUsuario = await Usuario.create({
    nombre: 'Juan',
    edad: 25,
    correo: 'juan@example.com',
  });
  
  console.log('Usuario creado:', nuevoUsuario.toJSON());
})();
```


## Lectura de Datos
```javascript
(async () => {
  const usuarios = await Usuario.findAll();
  console.log('Usuarios encontrados:', usuarios.map(u => u.toJSON()));
})();
```


## Actualización de Datos
```javascript
(async () => {
  await Usuario.update({ edad: 30 }, { where: { nombre: 'Juan' } });
})();
```


## Eliminación de Datos
```javascript
(async () => {
  await Usuario.destroy({ where: { nombre: 'Juan' } });
})();
```


