> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/comunicacion-sse-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Creación del Servidor SSE
```javascript
import http from 'http';

// Función para enviar eventos al cliente
function enviarEvento(res, evento, datos) {
  res.write(`event: ${evento}\n`);
  res.write(`data: ${JSON.stringify(datos)}\n\n`);
}

// Crear servidor HTTP
const server = http.createServer((req, res) => {
  // Encabezado para indicar que se envían eventos SSE
  res.writeHead(200, {
    'Content-Type': 'text/event-stream',
    'Cache-Control': 'no-cache',
    'Connection': 'keep-alive'
  });

  // Enviar un evento cada 5 segundos
  const intervalo = setInterval(() => {
    enviarEvento(res, 'mensaje', { mensaje: 'Hola desde el servidor' });
  }, 5000);

  // Manejar cierre de conexión del cliente
  req.on('close', () => {
    clearInterval(intervalo);
    console.log('Cliente desconectado');
  });
});

const puerto = 3030;
server.listen(puerto, () => {
  console.log(`Servidor SSE iniciado en http://localhost:${puerto}`);
});
```


## Cliente Web SSE (Frontend)
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Cliente SSE</title>
</head>
<body>
  <div id="mensaje"></div>

  <script>
    const mensajeDiv = document.getElementById('mensaje');

    const evtSource = new EventSource('http://localhost:3030');

    evtSource.onmessage = function(event) {
      const datos = JSON.parse(event.data);
      mensajeDiv.innerHTML = 'Mensaje del servidor: ' + datos.mensaje;
    };

    evtSource.onerror = function(event) {
      console.error('Error de SSE:', event);
      evtSource.close();
    };
  </script>
</body>
</html>
```


