> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/consumir-api-rest-con-axios-y-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Cómo usar axios
```bash
npm install axios
```


## Ejemplo de Consumo de una API RESTful
```javascript
const axios = require('axios');

// Realizar una petición GET para obtener todos los usuarios
axios.get('http://localhost:3000/usuarios')
  .then((response) => {
    // Manejar la respuesta exitosa
    console.log('Usuarios:', response.data);
  })
  .catch((error) => {
    // Manejar el error en caso de fallo
    console.error('Error al obtener usuarios:', error);
  });
```


