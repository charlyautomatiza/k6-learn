# La interfaz de línea de comandos de k6 (CLI)

---

## Comandos

Los tres comandos más comunes son:

| Comando   | Descripción                    | Uso            |
| --------- | ------------------------------ | ---------------- |
| `help`    | Muestra todos los comandos posibles | `k6 help`        |
| `run`     | Ejecuta un script k6           | `k6 run test.js` |
| `version` | Muestra la versión k6 instalada  | `k6 version`     |

---

## Flags

| Flag                   | Descripción                                                    | Uso                                    |
| ---------------------- | -------------------------------------------------------------- | ---------------------------------------- |
| `--help`               | Muestra las posibles banderas para el comando dado                  | `k6 run --help`                          |
| `--vus` o `-u`        | Establece el número de usuarios virtuales                                   | `k6 run test.js --vus 10 --duration 30s` |
| `--duration`           | Establece la duración de la prueba                                  | `k6 run test.js --duration 10m`          |

---

| Flag                   | Descripción                                                    | Uso                                    |
| ---------------------- | -------------------------------------------------------------- | ---------------------------------------- |
| `--iterations` o `-i` | Indica a k6 que itere la función por defecto un número de veces | `k6 run test.js -i 3`                    |
| `-e`                   | Establece una variable de entorno para pasar al script             | `k6 run test.js -e DOMAIN=test.k6.io`                           

---

## Obteniendo ayuda: `help`

Al ejecutar `k6 help` se obtiene lo siguiente:

```shell
          /\      |‾‾| /‾‾/   /‾‾/
     /\  /  \     |  |/  /   /  /
    /  \/    \    |     (   /   ‾‾\
   /          \   |  |\  \ |  (‾)  |
  / __________ \  |__| \__\ \_____/ .io

Usage:
  k6 [command]

Available Commands:
  archive     Create an archive
  cloud       Run a test on the cloud
  convert     Convert a HAR file to a k6 script
  help        Help about any command
  inspect     Inspect a script or archive
  login       Authenticate with a service
  pause       Pause a running test
  resume      Resume a paused test
  run         Start a load test
  scale       Scale a running test
  stats       Show test metrics
  status      Show test status
  version     Show application version

Flags:
  -a, --address string      address for the api server (default "localhost:6565")
  -c, --config string       JSON config file (default "/Users/nic/Library/Application Support/loadimpact/k6/config.json")
  -h, --help                help for k6
      --log-output string   change the output for k6 logs, possible values are stderr,stdout,none,loki[=host:port] (default "stderr")
      --log-format string   log output format
      --no-color            disable colored output
  -q, --quiet               disable progress updates
  -v, --verbose             enable verbose logging

Use "k6 [command] --help" for more information about a command.
```

---

## Ejecución y opciones de ejecución: `run`

Otro comando común de k6 es `k6 run [nombre_archivo].js`.

---

### El indicador de duración

La duración especifica el tiempo de ejecución de la prueba. Puede definirla en la línea de comandos con el indicador `--duration`:

```shell
k6 run test.js --duration 30s
```

Puede utilizar `s` (segundos), `h` (horas) y `m` (minutos) para definir la duración.

---

### La flag de iteraciones

Puedes establecer el número de iteraciones con la flag `--iterations` o `-i`, así:

```shell
k6 run test.js --iterations 100
k6 run test.js -i 100
```

---

### Flags de usuarios virtuales

Puede ajustar el número de usuarios virtuales con la flag `-u` o `--vus` al ejecutar la prueba:

```shell
k6 run test.js --vus 10 --duration 1m
k6 run test.js -u 10 --iterations 100
```

---

### Variables de entorno

Para utilizar una variable de entorno, defina la variable en su script:

```js [3|5-7]
import http from 'k6/http';

const hostname = `http://${__ENV.DOMAIN}`;

export default function () {
    let res = http.get(hostname + '/my_messages.php');
}
```

---

A continuación se explica cómo definirlo en tiempo de ejecución:

```shell
k6 run test.js -e DOMAIN=test.k6.io
```

---

## Cambio de ajustes en k6

k6 siempre [prioriza los ajustes](https://k6.io/docs/using-k6/k6-options/how-to/#order-of-precedence) en este orden:

![Priority of configurations and settings in k6](../../images/k6-order-of-preference-settings.png)
<!-- .element class="stretch" -->

---

## Entendiendo los resultados de k6

- Siguiente capítulo: [06-understanding-k6-results](?p=esp/06-understanding-k6-results)

