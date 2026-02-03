---
icon: square-small
---

# Personalización de L1

Una de las mayores ventajas de crear L1s en Avalanche es la capacidad de personalización completa. A diferencia de otros exosistemas donde debes adaptarte a un conjunto limitado de reglas y tecnologías, en Avalanche puedes definir desde el consenso hasta el lenguaje de programación y las reglas de acceso a la red.

Esto permite que la infraestructura se ajuste a las necesidades del proyecto, tienes la posibilidad de "clonar" una blockchain altamente eficaz y personalizarla a tu gusto, aprovechando el rendimiento, seguridad y experiencia de usuario que hay en el ecosistema.&#x20;

## Capas de personalización

En avalanche podemos personalizar la blockchain en 3 niveles

* **Smart Contract:** Puedes elegir en qué **lenguaje** desarrollar la lógica de la red.
* **Execution:** Se puede seleccionar el **motor de ejecución** que procesará las transacciones.
* **Consensus:** Todas las blockchains de Avalanche se benefician del **Avalanche Consensus**, un protocolo extremadamente rápido, seguro y eficiente energéticamente.

<figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

## Tipos de personalización de VM

Tenemos 3 maneras de personalizar a nivel de ejecución:

<figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

## Control de permisos (Permissioning)

Avalanche permite definir quién puede:

* **Validar:**\
  Seleccionar que nodos participan en el consenso
* **Desplegar contratos inteligentes:**\
  Limitar quien puede desplegar nuevos contratos para evitar congestión o ataques
* **Usar la red:**\
  Crear listas de acceso para transacciones (KYC, socios autorizados, etc.)

Este control se logra mediante **allowlists** y configuración especifica en la VM, lo que permite cumplir regulaciones, proteger la economía de la red y evitar abusos.

<figure><img src="../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

Por ejemplo, un proyecto institucional o gubernamental puede requerir que la información no salga del país, y por ende, solo debes permitir que solo nodos validadores de ese determinado país puedan participar en el consenso.
