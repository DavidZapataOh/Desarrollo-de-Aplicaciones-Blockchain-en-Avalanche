---
icon: square-small
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Soluciones Layer 2

Si bien Ethereum es una plataforma poderosa, hemos visto que a veces puede volverse lenta y costosa, especialmente en momentos de alta demanda. Aquí es donde entran en juego las soluciones **Layer 2**, que buscan resolver estos problemas sin cambiar la estructura básica de Ethereum.

### ¿Qué es Layer 2?

**Layer 2** (Capa 2) se refiere a una serie de tecnologías que se construyen "encima" de la blockchain principal de Ethereum, que es conocida como **Layer 1**. Estas soluciones están diseñadas para mejorar la **escalabilidad**, reducir los **costos de transacción** y aumentar la **velocidad** sin comprometer la seguridad o la descentralización de la red principal.

En lugar de procesar cada transacción directamente en Ethereum (Layer 1), las soluciones Layer 2 permiten que muchas de esas transacciones ocurran fuera de la cadena principal y luego se agrupen o resuman para finalmente ser validadas en Ethereum. Esto alivia la carga en la red principal, haciendo que todo funcione de manera más eficiente.

### ¿Cómo funcionan las Soluciones Layer 2?

La idea detrás de Layer 2 es simple, en lugar de hacer que cada transacción pase por la blockchain principal de Ethereum, se pueden realizar transacciones "fuera de la cadena" y luego enviar solo la información final a Ethereum para su validación. Esto reduce la congestión en la red principal y hace que las transacciones sean más rápidas y baratas.

Existen varias implementaciones y tecnologías de Layer 2, pero los dos enfoques más populares son los **Rollups** y las **Sidechains**. Vamos a ver cómo funciona cada uno.

### Rollups

Los **rollups** son la solución Layer 2 más popular y efectiva. Funcionan agrupando un montón de transacciones en una sola operación y luego enviando esa operación condensada a la cadena principal de Ethereum.

Imagina que 100 personas quieren hacer transacciones en Ethereum. Si cada una de esas transacciones se procesara directamente en la red principal, el costo sería alto y podría llevar más tiempo. Con un **rollup**, esas 100 transacciones se agrupan y se procesan como una sola transacción en Ethereum. Esto reduce la cantidad de datos que se necesita almacenar y procesar en la blockchain principal, haciendo que las tarifas sean mucho más bajas.

Existen dos tipos principales de rollups:

1. **Optimistic Rollups**: Estos rollups asumen que las transacciones son válidas, pero permiten que los usuarios puedan impugnar las transacciones si sospechan que algo no está bien. Si alguien impugna con éxito una transacción, se corrige y se penaliza a quienes intentaron hacer trampa.
2. **ZK-Rollups**: Estos rollups utilizan algo llamado "**pruebas de conocimiento cero**" (Zero-Knowledge Proofs) para verificar que las transacciones sean válidas sin necesidad de procesarlas todas en Ethereum. Son más rápidos y eficientes, pero su implementación es más compleja.

Aquí puedes ver un listado de las L2 de Ethereum:

{% embed url="https://l2beat.com/scaling/summary" %}

### Sidechains

Otra solución Layer 2 son las **sidechains**. A diferencia de los rollups, las sidechains son cadenas de bloques completamente separadas que se ejecutan junto a Ethereum. Estas cadenas tienen sus propias reglas y mecanismos de consenso, pero están diseñadas para ser compatibles con Ethereum, lo que significa que los usuarios pueden mover sus activos entre la sidechain y Ethereum cuando lo deseen.

Una de las sidechains más conocidas es **Polygon**, que permite a los usuarios realizar transacciones de manera mucho más rápida y barata que en la red principal de Ethereum. Los activos se pueden mover entre Polygon y Ethereum, lo que permite a los usuarios disfrutar de lo mejor de ambos mundos: la escalabilidad de Polygon y la seguridad de Ethereum.

### ¿Por qué son necesarias en Ethereum?

El principal problema que resuelven las soluciones Layer 2 es la **escalabilidad**. Como mencionamos en secciones anteriores, Ethereum en su forma original (Layer 1), tiene una capacidad limitada para procesar transacciones. Cuando la demanda aumenta, la red se congestiona, lo que hace que las tarifas de gas se disparen y las transacciones se ralenticen.

Layer 2 aborda este problema directamente al reducir la cantidad de transacciones que necesitan ser procesadas en la cadena principal, lo que **mejora la velocidad** y **reduce los costos** sin comprometer la seguridad.

Además, con el aumento de aplicaciones descentralizadas, la necesidad de soluciones escalables es más importante que nunca. Layer 2 permite que Ethereum siga siendo una de las plataformas principales para crear tu proyecto blockchain sin que los usuarios tengan que lidiar con tarifas prohibitivas o largas esperas.
