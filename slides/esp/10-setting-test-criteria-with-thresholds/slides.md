# k6 Thresholds

---

## Agregando umbrales (thresholds) a nuestro script

```js [7-10]
export let options = {
  stages: [
    { duration: '30m', target: 100 },
    { duration: '1h', target: 100 },
    { duration: '5m', target: 0 },
  ],
  thresholds: {
    http_req_failed: ['rate<=0.05'],
    http_req_duration: ['p(95)<=5000'],
  },
};
```

---

> 💡 Thresholds son **siempre** basados on metricas.

---

## Tipos de thresholds

- Error rate
- Response time
- Checks

> 💡 Recomendado: Usar error rate, response time, y checks thresholds en tus tests donde sea posible.

---

### Tasa de error (Error rate)

```js
thresholds: {
    http_req_failed: ['rate<=0.05'],
},
```

---

### Tiempo de respuesta (Response time)

```js
thresholds: {
    http_req_duration: ['p(95)<=5000'],
},
```

> 💡 Recomendado: Empezar con el percentil 95 del tiempo de respuesta. 

---

#### Usando multiples thresholds para tiempo de respuesta

```js
thresholds: {
    http_req_duration: ['p(90) < 400', 'p(95) < 800', 'p(99.9) < 2000'],
},
```

---

### Checks

```js
thresholds: {
  checks: ['rate>=0.9'],
},
```

---

## Finalizando pruebas ante fallos

```js
thresholds: {
    http_req_failed: [{
      threshold: 'rate<=0.05',
      abortOnFail: true,
    }],
},
```

---

## El script completo

```js
import http from 'k6/http';
import { check, sleep } from 'k6';

export let options = {
  stages: [
    { duration: '30m', target: 100 },
    { duration: '1h', target: 100 },
    { duration: '5m', target: 0 },
  ],
  thresholds: {
    http_req_failed: [{
      threshold: 'rate<=0.05',
      abortOnFail: true,
    }],
    http_req_duration: ['p(95)<=100'],
    checks: ['rate>=0.99'],
  },
};

export default function() {
  let url = 'https://httpbin.test.k6.io/post';
  let response = http.post(url, 'Hello world!');
  check(response, {
      'Application says hello': (r) => r.body.includes('Hello world!')
  });

  sleep(Math.random() * 5);
}
```

---

## Salida de resultados k6 de diferentes formas

- Siguiente capitulo: [11-k6-results-output-options](?p=esp/11-k6-results-output-options)