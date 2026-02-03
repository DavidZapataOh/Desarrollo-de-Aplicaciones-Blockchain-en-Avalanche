---
icon: square-small
---

# Avalanche L1 vs L2

Cuando hablamos de escalar y personalizar blockchains es común que se confundan las soluciones L1 con las de L2. Aunque ambas buscan mejorar capacidades y rendimiento, la forma en la que lo logran y las posibilidades que ofrecen son muy diferentes.

En el caso de Avalanche, lo que creamos con una blockchain personalizada son L1 independientes, no L2.

## 1. Arquitectura y dependencia

*   Avalanche L1s:

    Cada L1 creada en Avalanche es una blockchain completamente diferente, con su propio conjunto de validadores, reglas, token nativo y configuración. No depende de otra blockchain para su seguridad o procesamiento, aunque puede interactuar con otra mediante puentes o mensajería interchain.
* L2:\
  Una L2 se construye encima de una L1 existente y hereda su seguridad. No es independiente, necesita a la L1 subyacente para validar el estado final de sus transacciones.

## 2. Seguridad

* Avalanche L1s: \
  La seguridad la define la propia L1, ya sea mediante sus propios validadores o aprovechando la seguridad compartida de la red principal de Avalanche si así se configura. Esto da flexibilidad para ajustar el nivel de descentralización, costos y rendimiento.
* L2:\
  Toda su seguridad proviene de la L1 en la que está construida. Si la L1 tiene un problema, la L2 también lo sufre.

## 3. Personalización

* Avalanche L1s:\
  Permiten modificar desde el mecanismo de consenso hasta las reglas economicas, el tamaño de bloque, la maquina virtual, la lógica de ejecución y el token nativo. Son ideales para casos de uso específicos que requieren optimización a nivel de protocolo.
* L2:\
  La personalización es más limitada porque deben ser compatibles con la L1 en la que se ejecutan. Por ejemplo, una L2 sobre Ethereum tiene que ejecutarse a la lógica EVM y las limitaciones de Ethereum.

## 4. Escalabilidad

* Avalanche L1s:\
  Cada L1 maneja sus propias transacciones  y no compite por el espacio de bloque con otras L1, lo que evita congestión y mantiene las tarifas bajas.
* L2:\
  Mejoran el rendimiento de la L1 al procesar transacciones fuera de la cadena principal, pero aún dependen de publicar datos o pruebas en la L1, lo que puede generar cuellos de botella si la L1 se congestiona.
