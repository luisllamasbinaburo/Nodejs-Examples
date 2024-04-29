> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/comunicacion-udp-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Ejemplo de implementación de UDP en Node.js
```javascript
import dgram from 'dgram';

// Crear un servidor UDP
const server = dgram.createSocket('udp4');

// Evento al recibir un mensaje
server.on('message', (msg, rinfo) => {
  console.log(`Mensaje recibido desde ${rinfo.address}:${rinfo.port} - Contenido: ${msg}`);

  // Responder al cliente
  server.send('Mensaje recibido por el servidor', rinfo.port, rinfo.address, (err) => {
    if (err) {
      console.error('Error al enviar mensaje:', err);
    } else {
      console.log('Respuesta enviada al cliente');
    }
  });
});

// Evento cuando el servidor está listo y escuchando
server.on('listening', () => {
  const address = server.address();
  console.log(`Servidor UDP iniciado en ${address.address}:${address.port}`);
});

// Manejar errores
server.on('error', (err) => {
  console.error('Error en servidor UDP:', err);
  server.close();
});

const puerto = 3000;
server.bind(puerto);
```


