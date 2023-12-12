
<style>
  .container {
    display: flex;
  }

  .col {
    flex: 1;
  }
</style>

## Pruebas de Performance en el Frontend

![An example website with the title crocs r cool](../../images/frontend-performance.png)
<!-- .element class="stretch" -->

---

<div class="container">
  <div class="col">

### ¿Por qué las pruebas de rendimiento del frontend no son suficientes?

  - El rendimiento del frontend no mira bajo el capó
  - Sin carga, no prueba en condiciones de tráfico
  - Las pruebas de carga a nivel de navegador consumen muchos recursos y son costosas

  </div>

  <div class="col">

  ![Un gráfico que muestra que las pruebas de carga de los navegadores son costosas y consumen muchos recursos](../../images/frontend-limitations.png)

  </div>
</div>

---

![Gráfico que agrega los tiempos de respuesta del frontend y del backend. A medida que aumenta la concurrencia, el tiempo de respuesta del backend es mucho mayor.](../../images/frontend-backend.png)

---

## Backend performance testing

![Un componente de un sistema backend](../../images/backend-component.png)
<!-- .element class="stretch" -->

---

## ¿Qué verificamos del rendimiento del backend?

- **Escalabilidad**
- **Elasticidad**
- **Disponibilidad** 
- **Fiabilidad**
- **Resistencia**
- **Latencia**

---

<div class="container">
  <div class="col">

### ¿Por qué las pruebas de rendimiento del backend no son suficientes?

  - Ignora la experiencia del usuario
  - Los scripts pueden ser largos de crear 
  - Más difíciles de mantener

  </div>

  <div class="col">

  ![Un gráfico que muestra que las pruebas de carga de los navegadores son costosas y consumen muchos recursos](../../images/frontend-limitations.png)

  </div>
</div>

---

## Load testing

- Siguiente capítulo: [03-load-testing](?p=esp/03-load-testing)

