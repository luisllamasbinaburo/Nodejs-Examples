> Códigos de ejemplo de los tutoriales de www.luisllamas.es
>
> Enlace entrada: https://www.luisllamas.es/como-trabajar-con-threads-nodejs/
>
> Todo el contenido distribuido bajo licencia CCC, salvo indicación expresa

## Ejemplo básico
```javascript
import { Worker, isMainThread, workerData, parentPort } from 'node:worker_threads';

// Verifica si el hilo actual es el hilo principal
if (isMainThread) {
  // Si es el hilo principal, se define un conjunto de datos
  const data = 'some data';
  // Se crea un nuevo hilo de trabajo y se le pasa los datos definidos
  const worker = new Worker(import.meta.filename, { workerData: data });
  // Se escucha por mensajes enviados desde el hilo de trabajo
  worker.on('message', msg => console.log('Reply from Thread:', msg));
} else {
  // Si no es el hilo principal, se obtienen los datos pasados al hilo de trabajo
  const source = workerData;
  // Se convierte el texto a mayúsculas y luego se codifica a base64
  parentPort.postMessage(btoa(source.toUpperCase()));
}
```


## Ejemplo: Cálculo de números primos en paralelo
```javascript
// primeCalculator.js
import { Worker, isMainThread, parentPort, workerData } from 'node:worker_threads';

function isPrime(num) {
  if (num <= 1) return false;
  if (num <= 3) return true;
  if (num % 2 === 0 || num % 3 === 0) return false;
  let i = 5;
  while (i * i <= num) {
    if (num % i === 0 || num % (i + 2) === 0) return false;
    i += 6;
  }
  return true;
}

if (isMainThread) {
  const min = 2;
  const max = 100000;
  const numThreads = 4;
  const range = Math.ceil((max - min) / numThreads);

  for (let i = 0; i < numThreads; i++) {
    const start = min + range * i;
    const end = i === numThreads - 1 ? max : start + range;
    const worker = new Worker(__filename, {
      workerData: { start, end },
    });
    worker.on('message', (message) => {
      console.log('Primes found:', message.primes);
    });
  }
} else {
  const { start, end } = workerData;
  const primes = [];
  for (let i = start; i < end; i++) {
    if (isPrime(i)) {
      primes.push(i);
    }
  }
  parentPort.postMessage({ primes });
}
```


## Ejemplo: Procesamiento de imágenes en paralelo
```javascript
import { Worker, isMainThread, parentPort, workerData } from 'node:worker_threads';
import { loadImage, processImage, saveImage } from './imageUtils.js';

if (isMainThread) {
  const imagePaths = [
    'image1.jpg',
    'image2.jpg',
    'image3.jpg',
    // Agregar más rutas de imágenes según sea necesario
  ];

  const numThreads = 4;
  const imagesPerThread = Math.ceil(imagePaths.length / numThreads);

  for (let i = 0; i < numThreads; i++) {
    const start = i * imagesPerThread;
    const end = start + imagesPerThread;
    const paths = imagePaths.slice(start, end);

    const worker = new Worker(__filename, {
      workerData: { paths },
    });

    worker.on('message', ({ processedImages }) => {
      console.log('Procesamiento de imágenes completo:', processedImages);
    });
  }
} else {
  const { paths } = workerData;
  const processedImages = [];

  paths.forEach(async (path) => {
    try {
      const image = await loadImage(path);
      const processedImage = await processImage(image);
      const savedPath = await saveImage(processedImage);
      processedImages.push(savedPath);
    } catch (error) {
      console.error('Error al procesar la imagen:', error);
    }
  });

  parentPort.postMessage({ processedImages });
}
```


