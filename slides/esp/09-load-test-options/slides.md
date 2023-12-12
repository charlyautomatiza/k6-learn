# k6 Load Test Options

---

## Opciones para los Scripts

```js
export let options = {
  vus: 10,
  iterations: 40,
};
```

---

> 💡 Si sólo defines VUs y ninguna otra opción de prueba, puedes obtener el siguiente error:

```shell
          /\      |‾‾| /‾‾/   /‾‾/   
     /\  /  \     |  |/  /   /  /    
    /  \/    \    |     (   /   ‾‾\  
   /          \   |  |\  \ |  (‾)  | 
  / __________ \  |__| \__\ \_____/ .io

WARN[0000] the `vus=10` option will be ignored, it only works in conjunction with `iterations`, `duration`, or `stages` 
  execution: local
     script: test.js
     output: -
```

---

## Iteraciones

```js
  vus: 10,
  iterations: 40,
```

> Establecer el número de iteraciones en las opciones de prueba lo define para **todos** los usuarios.

---

## Duración

```js
  vus: 10,
  duration: '2m'
```

> Al establecer la duración, k6 recibe instrucciones de repetir la secuencia de comandos para cada una de las VU hasta alcanzar la duración.

---

## Iteraciones and duraciones

```js
  vus: 10,
  duration: '5m',
  iterations: 40,
```

> Si establece la duración junto con el número de iteraciones, se utilizará el valor que termine antes.

---

## Stages

Definiendo las iteraciones y la duración creamos un _perfil de carga simple_.

![A simple load profile](../../images/load_profile-no_ramp-up_or_ramp-down.png)
<!-- .element class="stretch" -->

---

## Perfil de Carga constante

¿Y si quieres añadir tráfico ascendente o descendente para que el perfil se parezca más a esto?

![Constant load profile, with ramps](../../images/load_profile-constant.png.png)
<!-- .element class="stretch" -->

---

En ese caso, puede utilizar [stages](https://k6.io/docs/using-k6/options/#stages).

```js
export let options = {
  stages: [
    { duration: '30m', target: 100 },
    { duration: '1h', target: 100 },
    { duration: '5m', target: 0 },
  ],
};
```

---

## El script completo hasta ahora

Si estás usando stages, esto es lo que tu script debería tener:

```js
import http from 'k6/http';
import { check, sleep } from 'k6';

export let options = {
  stages: [
    { duration: '30m', target: 100 },
    { duration: '1h', target: 100 },
    { duration: '5m', target: 0 },
  ],
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

## Establezcamos algunos umbrales (thresholds)

- Siguiente capítulo: [10-setting-test-criteria-with-thresholds](?p=esp/10-setting-test-criteria-with-thresholds)