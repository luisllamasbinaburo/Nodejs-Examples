> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/como-usar-socketio-y-express-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Cómo usar Express junto Socket.IO
```bash
npm install express socket.io http
```


## Configuración del Servidor
```javascript
import express from 'express';
import http from 'http';
import { Server as SocketIOServer } from 'socket.io';

const app = express();
const server = http.createServer(app);
const io = new SocketIOServer(server, { cors: { origin: '*' } }); // cors solo para test en el ejemplo!

// Servir archivos estáticos desde la carpeta 'public'
app.use(express.static('public'));

// Manejar conexiones de clientes
io.on('connection', (socket) => {
  console.log('Cliente conectado');

  // Manejar mensajes del cliente
  socket.on('message', (message) => {
    console.log('Mensaje recibido:', message);
    
    // Enviar mensaje a todos los clientes, incluido el que envió el mensaje
    io.emit('message', message);
  });

  // Manejar desconexiones
  socket.on('disconnect', () => {
    console.log('Cliente desconectado');
  });
});

const PORT = process.env.PORT || 3000;
server.listen(PORT, () => {
  console.log(`Servidor Socket.IO iniciado en http://localhost:${PORT}`);
});
```


## Paso 1: Crear la Interfaz de Usuario
```html
<!-- public/index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Chat con Socket.IO</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/socket.io/4.7.5/socket.io.js" integrity="sha512-luMnTJZ7oEchNDZAtQhgjomP1eZefnl82ruTH/3Oj/Yu5qYtwL7+dVRccACS/Snp1lFXq188XFipHKYE75IaQQ==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
  <script src="client.js"></script>
</head>
<body>
  <h1>Chat con Socket.IO</h1>
  <ul id="messages"></ul>
  <input type="text" id="message" placeholder="Escribe un mensaje...">
  <button onclick="sendMessage()">Enviar</button>
</body>
</html>
```

```javascript
const socket = io.connect('http://localhost:3000');

// Enviar mensaje al servidor
function sendMessage() {
  const message = document.getElementById('message').value;
  socket.emit('message', message);
  document.getElementById('message').value = '';
}

// Recibir mensajes del servidor
socket.on('message', function(message) {
  const newMessage = document.createElement('li');
  newMessage.textContent = message;
  document.getElementById('messages').appendChild(newMessage);
});
```


## Ejecutar la Aplicación
```bash
node server.js
```


