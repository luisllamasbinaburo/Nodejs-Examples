> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/criptografia-en-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Generar un Hash de una cadena
```javascript
import { createHash } from 'node:crypto';

const cadena = 'Mensaje a hash';

const hash = createHash('sha256');
hash.update(cadena);

const hashResultado = hash.digest('hex');
console.log('Hash SHA-256:', hashResultado);
```


## Generar un Hash de una contraseña con Sal
```javascript
import { hashSync, compareSync, genSaltSync } from 'bcrypt';

const password = 'contraseña123';

// Generar hash con sal
const saltRounds = 10;
const salt = genSaltSync(saltRounds);
const hash = hashSync(password, salt);

console.log('Hash de la contraseña:', hash);

// Comparar hash con contraseña ingresada
const contraseñaCorrecta = 'contraseña123';
const resultadoComparacion = compareSync(contraseñaCorrecta, hash);
console.log('Las contraseñas coinciden:', resultadoComparacion);
```


## Generar un par de claves RSA
```javascript
import { generateKeyPairSync } from 'node:crypto';

const { publicKey, privateKey } = generateKeyPairSync('rsa', {
  modulusLength: 2048,
  publicKeyEncoding: {
    type: 'spki',
    format: 'pem'
  },
  privateKeyEncoding: {
    type: 'pkcs8',
    format: 'pem'
  }
});

console.log('Clave Pública RSA:', publicKey);
console.log('Clave Privada RSA:', privateKey);
```


## Cifrar y descifrar datos utilizando RSA
```javascript
import { publicEncrypt, privateDecrypt } from 'node:crypto';

const mensaje = 'Mensaje a cifrar';

// Cifrar con clave pública
const mensajeCifrado = publicEncrypt(publicKey, Buffer.from(mensaje, 'utf8'));
console.log('Mensaje cifrado:', mensajeCifrado.toString('base64'));

// Descifrar con clave privada
const mensajeDescifrado = privateDecrypt(privateKey, mensajeCifrado);
console.log('Mensaje descifrado:', mensajeDescifrado.toString('utf8'));
```


