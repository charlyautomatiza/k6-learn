# k6 checks

---

## Nuestro script

```js
import http from 'k6/http';

export default function() {
  let url = 'https://httpbin.test.k6.io/post';
  let response = http.post(url, 'Hello world!');

  console.log(response.json().data);
}
```

---

## Agregamos checks a nuestro script

```js [1-5|6-8]
import http from 'k6/http';

export default function() {
  let url = 'https://httpbin.test.k6.io/post';
  let response = http.post(url, 'Hello world!');
  check(response, {
    'Application says hello': (r) => r.body.includes('Hello world!')
  });
  console.log(response.json().data);
}
```

---

```js
import http from 'k6/http';

export default function() {
  let url = 'https://httpbin.test.k6.io/post';
  let response = http.post(url, 'Hello world!');
  check(response, {
    'Application says hello': (r) => r.body.includes('Hello world!')
  });
  console.log(response.json().data);
}
```

---

## ¡Volvamos a ejecutar nuestra prueba!

Recuerdas el comando para ejecutar la prueba? 👀

```shell
	✓ Application says hello

     checks.........................: 100.00% ✓ 1        ✗ 0
```

---

## Checks fallidos

```js
check(response, {
      'Application says hello': (r) => r.body.includes('Bonjour!')
});
```

---

## Volvamos a realizar la prueba.

```shell
     ✗ Application says hello
      ↳  0% — ✓ 0 / ✗ 1

     checks.........................: 0.00%  ✓ 0        ✗ 1
```

---

## ¡Las comprobaciones fallidas no son errores!

> 💡 Para que las comprobaciones fallidas detengan la prueba, puede [combinarlas con umbrales (thresholds)](https://k6.io/docs/using-k6/thresholds/#failing-a-load-test-using-checks).

---

## Haciendo tus scripts realistas con tiempos de espera

- Siguiente capítulo: [08-adding-think-time](?p=esp/08-adding-think-time)