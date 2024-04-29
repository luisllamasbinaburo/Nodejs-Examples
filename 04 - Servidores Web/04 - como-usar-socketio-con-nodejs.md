> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/como-usar-socketio-con-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Configuración del Servidor Socket.IO
```bash
npm install express socket.io
```


## Configurar el servidor
```javascript
import { createServer } from 'http';
import { Server as SocketIOServer } from 'socket.io';

const server = createServer();
const io = new SocketIOServer(server, { cors: { origin: '*' } }); // cors ¡solo para test en el desarrollo!

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


## Creación del Cliente Web
```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Chat en Tiempo Real con Socket.IO</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/socket.io/4.7.5/socket.io.js" integrity="sha512-luMnTJZ7oEchNDZAtQhgjomP1eZefnl82ruTH/3Oj/Yu5qYtwL7+dVRccACS/Snp1lFXq188XFipHKYE75IaQQ==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <h1>Chat en Tiempo Real con Socket.IO</h1>
  <ul id="messages"></ul>
  <input type="text" id="message" placeholder="Escribe un mensaje...">
  <button onclick="sendMessage()">Enviar</button>

  <script src="client.js"></script>
</body>
</html>
```

```css
body {
  font-family: Arial, sans-serif;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin-bottom: 5px;
}

input[type="text"] {
  width: 200px;
  padding: 5px;
  margin-right: 5px;
}

button {
  padding: 5px 10px;
  cursor: pointer;
}
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


