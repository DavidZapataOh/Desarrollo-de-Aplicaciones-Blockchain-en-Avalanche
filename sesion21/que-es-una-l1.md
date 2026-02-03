---
icon: square-small
---

# Qué es una L1

En blockchain, el término **layer** (capa) se utiliza para describir diferentes **niveles de infraestructura y funcionalidades**. Cada capa tiene un propósito especifico dentro de la arquitectura y ayuda a resolver problemas concretos como la seguridad, escalabilidad o usabilidad.

Antes de entrar en detalle, es importante aclarar que en Avalanche lo que creamos al desarrollar una blockchain personalizada es una Layer 1 (L1), antes llamadas subnets.

## Layer (L0) - La red de redes

La Layer 0 es la base sobre cual se construyen las blockchains.\
Proporciona la infraestructura que permite que diferentes L1 se conecten, comuniquen e intercambien información o activos.

Un L0 no es una blockchain de uso general como tal, sino un protocolo o red que sirve como "capa de transporte" para multiples L1. Esto incluye funcionalidades como:

* **Interoperabilidad nativa** entre chains
* **Seguridad compartida** para las blockchains que se construyen sobre ella
* **Protocolos de comunicación interchain**

## Layer 1 (L1) - Blockchain Independiente

La L1 es una blockchain que define sus propias reglas, consenso, validadores y activos nativos. Aquí se procesan directamente las transacciones y, en muchos casos, se ejecutan contratos inteligentes.

Bitcoin y Ethereum son L1 independientes, mientras que en Avalanche cada blockchain que creamos es también una L1, con su propio conjunto de validadores, tokens y configuraciones de red. Brindando estas caracteristicas:

* Seguridad propia o compartida (según el modelo)
* Mecanismo de consenso definido (PoW, PoS, PoA, Snowman, etc)
* Capacidad para emitir su token nativo
* Ejecución directa de transacciones y contrates inteligentes

## Layer 2 (L2) - Escalando sobre una L1

Una L2 es una solución construida encima de una L1 para mejorar su rendimiento, reduciendo costos y aumentando velocidad sin comprometer la seguridad de la capa base.

Las L2 procesan transacciones fuera de la cadena principal y luego publican pruebas en la L1, heredando su seguridad.

Hay varios tipos de L2:

* Rollups (Optimistic y ZK)
* Sidechains (aunque en sentido estricto no siempre se consideran L2)
* State Channels



En resumen:

* **L0** es la infraestructura que conecta múltiples blockchains.
* **L1** es un blockchain independiente con seguridad y consenso propios.
* **L2** es una solución que mejora escalabilidad y costos de una L1.
