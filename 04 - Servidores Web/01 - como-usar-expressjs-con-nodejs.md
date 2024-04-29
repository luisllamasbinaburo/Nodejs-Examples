> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/como-usar-expressjs-con-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Instalación de Express.js
```bash
npm install express
```

```javascript
const express = require('express');
const app = express();
const PORT = 3000; // Puerto en el que escuchará el servidor

// aquí definiríamos las rutas
// ver más abajo

// Iniciar el servidor
app.listen(PORT, () => {
  console.log(`Servidor Express escuchando en el puerto ${PORT}`);
});
```


## Ejemplo de Ruta GET
```javascript
app.get('/', (req, res) => {
  res.send('¡Hola, mundo desde Express.js!');
});
```


## Ejemplo de Ruta POST
```javascript
app.post('/usuarios', (req, res) => {
  res.send('Información de usuario recibida y procesada');
});
```


## Ejemplo de Ruta Dinámica
```javascript
app.get('/usuarios/:id', (req, res) => {
  const { id } = req.params;
  res.send(`Solicitado usuario con ID: ${id}`);
});
```


## Ejemplo de Middleware de Registro de Solicitudes
```javascript
app.use((req, res, next) => {
  console.log(`Solicitud recibida en: ${req.url}`);
  next();
});
```


## Ejemplo de Middleware de Manejo de Errores
```javascript
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Algo salió mal');
});
```


## Ejemplo Completo de Aplicación Express.js
```javascript
const express = require('express');
const app = express();
const PORT = 3000;

// Middleware de registro de solicitudes
app.use((req, res, next) => {
  console.log(`Solicitud recibida en: ${req.url}`);
  next();
});

// Ruta GET en la raíz
app.get('/', (req, res) => {
  res.send('¡Hola, mundo desde Express.js!');
});

// Ruta POST para usuarios
app.post('/usuarios', (req, res) => {
  res.send('Información de usuario recibida y procesada');
});

// Ruta dinámica para usuarios
app.get('/usuarios/:id', (req, res) => {
  const { id } = req.params;
  res.send(`Solicitado usuario con ID: ${id}`);
});

// Middleware de manejo de errores
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Algo salió mal');
});

// Iniciar el servidor
app.listen(PORT, () => {
  console.log(`Servidor Express escuchando en el puerto ${PORT}`);
});
```


