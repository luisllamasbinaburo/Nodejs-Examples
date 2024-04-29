> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/alternativas-a-expressjs-en-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Koa
```javascript
import Koa from 'koa';
const app = new Koa();

app.use(async (ctx) => {
  ctx.body = '¡Hola, Koa!';
});

app.listen(3000);
```


## Hapi
```javascript
import Hapi from '@hapi/hapi';

const init = async () => {
  const server = Hapi.server({
    port: 3000,
    host: 'localhost'
  });

  server.route({
    method: 'GET',
    path: '/',
    handler: (request, h) => {
      return '¡Hola, Hapi!';
    }
  });

  await server.start();
  console.log('Servidor iniciado en:', server.info.uri);
};

init();
```


## Fastify
```javascript
import fastify from 'fastify';

const app = fastify({ logger: true });

app.get('/', async (request, reply) => {
  return { hello: 'world' };
});

app.listen(3000, (err, address) => {
  if (err) throw err;
  console.log(`Servidor iniciado en: ${address}`);
});
```


## NestJS
```typescript
// main.ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```


## AdonisJS
```javascript
// server.js
import { Ignitor } from '@adonisjs/ignitor';

new Ignitor(require('@adonisjs/fold'))
  .appRoot(__dirname)
  .fireHttpServer()
  .catch(console.error);
```


