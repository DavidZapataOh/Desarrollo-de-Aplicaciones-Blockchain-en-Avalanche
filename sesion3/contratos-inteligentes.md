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

# Contratos Inteligentes

Un **contrato inteligente** es básicamente un programa informático que se ejecuta en la blockchain. Pero lo que lo hace especial es que este programa sigue una serie de reglas predefinidas y, una vez que se cumplen ciertas condiciones, se ejecuta automáticamente, sin necesidad de que nadie lo supervise.

Para entenderlo de manera más simple, imagina que un contrato inteligente es como una **máquina expendedora**. Tú introduces una cantidad de dinero, seleccionas lo que deseas comprar, y la máquina te entrega el producto. Todo el proceso ocurre sin que nadie tenga que intervenir. El contrato inteligente funciona de manera similar, si se cumplen las condiciones (como introducir la cantidad correcta de dinero), automáticamente ejecuta lo que está programado (en este caso, entregar el producto).

<figure><img src="../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

### ¿Cómo funciona?

En la red de Ethereum los contratos inteligentes son el motor de las **dApps** (aplicaciones descentralizadas) y permiten que cualquier persona cree reglas y las haga cumplir de manera automática. Estos contratos están escritos en un lenguaje de programación llamado **Solidity**, que fue diseñado específicamente para crear contratos inteligentes en Ethereum.

Una vez que el contrato está escrito, se despliega en la blockchain y se convierte en algo inmutable. Esto significa que una vez que está en la blockchain, **nadie puede cambiarlo ni manipularlo**. Cualquier transacción que interactúe con ese contrato seguirá las reglas que se establecieron desde el principio.

Por ejemplo, imagina un contrato inteligente que dice: "si Juan envía 5 AVAX a este contrato, entonces el contrato le enviará un NFT". Una vez que Juan envíe los 5 AVAX, el contrato automáticamente le enviará el NFT, sin que ninguna persona tenga que intervenir para verificar o aprobar la transacción. Esto es lo que hace que los contratos inteligentes sean tan potentes, eliminan la necesidad de intermediarios y funcionan de manera completamente automatizada.

### Riesgos

Aunque los contratos inteligentes ofrecen un enorme potencial, no son perfectos. Al estar basados en código, **un error en el código puede tener consecuencias graves**. Un ejemplo famoso es el hackeo de **The DAO** en 2016, donde un error en el contrato inteligente permitió a un atacante drenar millones de dólares de la organización.

Este incidente dejó claro que aunque los contratos inteligentes eliminan a los intermediarios, también introducen nuevos riesgos, si el código no es seguro puede ser explotado. Por eso es crucial que los contratos sean auditados y revisados antes de ser desplegados en la blockchain.

### Contratos inteligentes en otras redes

Aunque Ethereum fue la primera red en popularizar los contratos inteligentes, no es la única que los utiliza. Otras blockchains como **Avalanche**, **Binance Smart Chain**, **Starknet** y **Solana**, también permiten el uso de contratos inteligentes. De hecho muchas de estas redes son compatibles con la **EVM** (Ethereum Virtual Machine), lo que significa que los contratos inteligentes escritos para Ethereum pueden ser ejecutados en otras plataformas sin mucho esfuerzo adicional.
