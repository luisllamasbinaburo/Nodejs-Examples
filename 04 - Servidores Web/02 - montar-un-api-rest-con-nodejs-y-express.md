> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/montar-un-api-rest-con-nodejs-y-express/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Creando nuestro API REST
```bash
npm install express
```

```js
// Cargar modulos y crear nueva aplicacion
var express = require("express"); 
var cors = require('cors')
var app = express();
app.use(cors())

var bodyParser = require('body-parser');
app.use(bodyParser.json()); // support json encoded bodies
app.use(bodyParser.urlencoded({ extended: true })); // support encoded bodies

//GetAll
//Ejemplo: GET http://localhost:8080/item
app.get('/item', function(req, res, next) {
  if(req.query.filter) {
  next();
  return;
  }
  res.send('Get all');
  console.log('Get all');
});

//GetById
//Ejemplo: GET http://localhost:8080/item/10
app.get('/item/:id', function(req, res, next) {
  var itemId = req.params.id;
  res.send('Get ' + req.params.id);
  console.log('Get ' + req.params.id);
});

//GetFiltered
//Ejemplo: GET http://localhost:8080/item?filter=ABC
app.get('/item', function(req, res) {
  var filter = req.query.filter;
  res.send('Get filter ' + filter);
  console.log('Get filter ' + filter);
});

//Create
//Ejemplo: POST http://localhost:8080/item
app.post('/item', function(req, res) {
  var data = req.body.data;
  res.send('Add ' + data);
  console.log('Add ' + data);
});

//Replace
//Ejemplo: PUT http://localhost:8080/item/10
app.put('/item/:id', function(req, res) {
  var itemId = req.params.id;
  var data = req.body.data;
  res.send('Replace ' + itemId + ' with ' + data);
  console.log('Replace ' + itemId + ' with ' + data);
});

//Update
//Ejemplo: PATCH http://localhost:8080/item/10
app.patch('/item/:id', function(req, res) {
  var itemId = req.params.id;
  var data = req.body.data;
  res.send('Update ' + itemId + ' with ' + data);
  console.log('Update ' + itemId + ' with ' + data);
});

//Delete
//Ejemplo: DEL http://localhost:8080/item
app.delete('/item/:id', function(req, res) {
  var itemId = req.params.id;
  res.send('Delete ' + itemId);
  console.log('Delete ' + itemId);
});
  
var server = app.listen(8080, function () {
    console.log('Server is running..'); 
});
```

```bash
node App.js
```


