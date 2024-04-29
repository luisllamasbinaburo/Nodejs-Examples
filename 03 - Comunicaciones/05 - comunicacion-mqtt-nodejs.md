> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/comunicacion-mqtt-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Ejemplo de implementación de MQTT en Node.js
```bash
npm install mqtt
```


## Creación de un cliente MQTT
```javascript
import mqtt from 'mqtt';

// Conexión al broker MQTT
const client = mqtt.connect('mqtt://localhost:1883'); // Cambia por tu URL y puerto del broker

// Evento cuando se conecta al broker
client.on('connect', () => {
  console.log('Conectado al broker MQTT');

  // Suscribirse a un tema
  client.subscribe('mi/tema', (err) => {
    if (!err) {
      console.log('Suscrito al tema "mi/tema"');
    }
  });

  // Publicar un mensaje en un tema
  client.publish('mi/tema', 'Hola desde el cliente MQTT');
});

// Evento cuando se recibe un mensaje en el tema suscrito
client.on('message', (topic, message) => {
  console.log('Mensaje recibido en el tema:', topic);
  console.log('Contenido del mensaje:', message.toString());
});

// Manejo de errores
client.on('error', (err) => {
  console.error('Error en el cliente MQTT:', err);
});
```


## Cliente MQTT (solo Publicador)
```javascript
import mqtt from 'mqtt';

const client = mqtt.connect('mqtt://localhost:1883');

client.on('connect', () => {
  console.log('Conexión establecida');
  setInterval(() => {
    const temperatura = Math.floor(Math.random() * 50); // Generar temperatura aleatoria
    client.publish('temperatura', temperatura.toString());
    console.log(`Mensaje publicado en "temperatura": ${temperatura}`);
  }, 5000); // Publicar cada 5 segundos
});

client.on('error', (error) => {
  console.error('Error de conexión:', error);
});
```


## Cliente MQTT (solo suscriptor)
```javascript
const mqtt = require('mqtt');

const client = mqtt.connect('mqtt://localhost:1883');

client.on('connect', () => {
  console.log('Conexión establecida');
  client.subscribe('temperatura');
});

client.on('message', (topic, message) => {
  console.log(`Mensaje recibido en ${topic}: ${message.toString()}°C`);
});
```


## Cliente Web MQTT
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/paho-mqtt/1.2.2/mqttws31.min.js"></script>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Cliente MQTT en la Web</title>  
</head>
<body>
  <h1>Cliente MQTT en la Web</h1>
  <div id="messages"></div>

  <script src="./paho-mqtt.min.js" integrity="sha512-Y5n0fbohPllOQ21fTwM/h9sQQ/1a1h5KhweGhu2zwD8lAoJnTgVa7NIrFa1bRDIMQHixtyuRV2ubIx+qWbGdDA==" crossorigin="anonymous" referrerpolicy="no-referrer"></script>
  
  <script>
    // Crear un cliente MQTT
    const client = new Paho.Client('localhost', 1833, 'web_client');

    // Función para mostrar mensajes en la página
    function displayMessage(topic, message) {
      const messagesDiv = document.getElementById('messages');
      const messageElement = document.createElement('p');
      messageElement.textContent = `Tema: ${topic}, Mensaje: ${message}`;
      messagesDiv.appendChild(messageElement);
    }

    // Callback cuando el cliente se conecta
    function onConnect() {
      console.log('Conectado al broker MQTT desde la web');
      client.subscribe('mi/tema');
    }

    // Callback cuando llega un mensaje
    function onMessageArrived(message) {
      console.log('Mensaje recibido:', message.destinationName, message.payloadString);
      displayMessage(message.destinationName, message.payloadString);
    }

    // Callback cuando hay un error
    function onFailure(message) {
      console.error('Error en la conexión:', message.errorMessage);
    }

    // Configurar los callbacks
    client.onConnectionLost = onFailure;
    client.onMessageArrived = onMessageArrived;

    // Conectar al broker
    client.connect({ onSuccess: onConnect });

    // Publicar un mensaje cuando se haga clic en un botón (solo como ejemplo)
    function publishMessage() {
      const message = 'Hola desde la web MQTT';
      const topic = 'mi/tema';
      const messageObj = new Paho.Message(message);
      messageObj.destinationName = topic;
      client.send(messageObj);
    }
  </script>

  <!-- Botón de ejemplo para publicar un mensaje -->
  <button onclick="publishMessage()">Publicar Mensaje</button>

  
</body>
</html>
```


