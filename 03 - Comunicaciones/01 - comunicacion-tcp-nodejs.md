> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/comunicacion-tcp-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Servidor TCP básico
```javascript
import net from 'node:net';

// Crear servidor TCP
const server = net.createServer((socket) => {
  console.log('Cliente conectado');

  // Evento al recibir datos del cliente
  socket.on('data', (data) => {
    console.log('Datos recibidos:', data.toString());

    // Enviar datos de vuelta al cliente
    socket.write('Datos recibidos por el servidor: ' + data.toString());
  });

  // Evento cuando se cierra la conexión del cliente
  socket.on('close', () => {
    console.log('Cliente desconectado');
  });

  // Manejar errores de conexión
  socket.on('error', (err) => {
    console.error('Error en conexión:', err);
  });
});

const puerto = 3000;
server.listen(puerto, () => {
  console.log(`Servidor TCP iniciado en puerto ${puerto}`);
});
```


## Cliente TCP en Node.js
```javascript
import net from 'node:net';

const client = new net.Socket();

const puerto = 3000;
const host = 'localhost'; // Cambia por el host donde está el servidor

client.connect(puerto, host, () => {
  console.log('Conectado al servidor TCP');
  client.write('Hola desde el cliente TCP');
});

client.on('data', (data) => {
  console.log('Datos recibidos del servidor:', data.toString());
  client.end();
});

client.on('close', () => {
  console.log('Conexión cerrada');
});

client.on('error', (err) => {
  console.error('Error de conexión:', err);
});
```


