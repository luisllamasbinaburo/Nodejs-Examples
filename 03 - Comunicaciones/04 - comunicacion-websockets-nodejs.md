> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/comunicacion-websockets-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Ejemplo de implementación de Websockets en Node.js
```bash
npm install ws
```


## Creación de un Servidor WebSocket
```javascript
// Importar el módulo 'ws'
import { WebSocketServer } from 'ws'

// Crear un nuevo servidor WebSocket que escuche en el puerto 3030
const wss = new WebSocketServer({ port: 3030 });

// Evento cuando un cliente se conecta al servidor WebSocket
wss.on('connection', function connection(ws) {
  console.log('Cliente conectado');

  // Evento para manejar mensajes recibidos del cliente
  ws.on('message', function incoming(message) {
    console.log('Mensaje recibido: %s', message);

    // Enviar un mensaje de vuelta al cliente
    ws.send('Mensaje recibido por el servidor: ' + message);
  });

  // Evento cuando se cierra la conexión con el cliente
  ws.on('close', function close() {
    console.log('Cliente desconectado');
  });
});

console.log('Servidor WebSocket iniciado en ws://localhost:3030')
```


## Creación de un Cliente WebSocket básico
```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Cliente WebSocket</title>
</head>
<body>
  <script>
    const socket = new WebSocket('ws://localhost:3030');

    socket.onopen = () => {
      console.log('Conexión establecida');
      socket.send('¡Hola desde el cliente!');
    };

    socket.onmessage = (event) => {
      console.log('Mensaje recibido:', event.data);
    };

    socket.onclose = () => {
      console.log('Conexión cerrada');
    };
  </script>
</body>
</html>
```


## Creación de un Cliente WebSocket (Frontend)
```html
<!DOCTYPE html>
<html lang="en">
   <head>
     <meta charset="UTF-8">
     <title>WebSocket Example</title>
   </head>
   <body>
     <h1>WebSocket Example</h1>
     <div id="messages"></div>
     <form id="messageForm">
       <input type="text" id="messageInput" placeholder="Enter message">
       <button type="submit">Send</button>
     </form>

     <script>
       const messages = document.getElementById('messages');
       const messageForm = document.getElementById('messageForm');
       const messageInput = document.getElementById('messageInput');

       const socket = new WebSocket('ws://localhost:3030');

       socket.addEventListener('open', () => {
         console.log('Connected to WebSocket server');
       });

       socket.addEventListener('message', (event) => {
         const message = event.data;
         displayMessage(message);
       });

       messageForm.addEventListener('submit', (event) => {
         event.preventDefault();
         const message = messageInput.value;
         socket.send(message);
         messageInput.value = '';
       });

       function displayMessage(message) {
         const messageElement = document.createElement('div');
         messageElement.innerText = message;
         messages.appendChild(messageElement);
       }
     </script>
   </body>
</html>
```


