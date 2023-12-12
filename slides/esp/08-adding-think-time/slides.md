# Tiempo de espera (think time)

---

## ¿Qué es el tiempo de espera (think time)?

La cantidad de tiempo que un script hace una pausa durante la ejecución de la prueba para simular los retrasos que tienen los usuarios reales al utilizar una aplicación.

---

## ¿Cuándo debe utilizar tiempo de espera (think time)?

- Si su prueba sigue un flujo de usuario
- Si desea simular acciones que tardan cierto tiempo en llevarse a cabo
- Su generador de carga, o la máquina desde la que está ejecutando k6, muestra una utilización de CPU elevada (> 80%) durante la ejecución de la prueba.

---

## ¿Cuándo **NO** se debe utilizar el tiempo de espera?

- Desea realizar una [prueba de estrés](https://k6.io/docs/test-types/stress-testing/) 
- El Endpoint de la API que está probando experimenta una gran cantidad de solicitudes por segundo en producción que se producen sin retrasos
- Su generador de carga puede ejecutar su script de prueba sin cruzar la marca del 80% de utilización de CPU.

---

## k6 Sleep

```js [2|11]
import http from 'k6/http';
import { check, sleep } from 'k6';

export default function() {
  let url = 'https://httpbin.test.k6.io/post';
  let response = http.post(url, 'Hello world!');
  check(response, {
      'Application says hello': (r) => r.body.includes('Hello world!')
  });

  sleep(1);
}
```

---

**El tiempo de espera no afecta al tiempo de respuesta (`http_req_duration`); el tiempo de respuesta siempre se indica sin el tiempo de espera.Sin embargo, el tiempo de espera se incluye en la duración de la iteración.**

---

## Tiempo de espera dinámico

Un tiempo de espera dinámico es más realista y simula mejor a los usuarios reales.

---

### Random sleep

Una forma de implementar el tiempo de espera dinámico es utilizando la función de JavaScript `Math.random()`:

```js
sleep(Math.random() * 5);
```

---

### Random sleep between

```js [1|3]
import { randomIntBetween } from "https://jslib.k6.io/k6-utils/1.0.0/index.js";

sleep(randomIntBetween(1,5));
```

---

## ¿Cuánto tiempo de espera debe añadir?

La verdadera respuesta es: depende.

---

## Pasemos a escalar nuestras pruebas

- Siguiente capítulo: [09-load-test-options](?p=esp/09-load-test-options)