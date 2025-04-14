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

# Qué es un ERC

Un **ERC** (Ethereum Request for Comments) es como un manual de instrucciones para construir diferentes tipos de contratos inteligentes en la blockchain de Ethereum. Imagina un conjunto de reglas o estándares que todos los desarrolladores siguen para asegurarse de que sus contratos funcionen de manera coherente y puedan interactuar fácilmente entre sí. Cada ERC describe cómo debe comportarse un contrato inteligente para cumplir con ciertas funcionalidades, como crear tokens, implementar NFTs o gestionar permisos y roles.

Son los planos y guías que todos deben seguir para garantizar que, por ejemplo, un token creado por un desarrollador pueda ser reconocido y utilizado por las aplicaciones de otro desarrollador.

### ¿Cómo se crean los ERC?

Los ERC se proponen como mejoras al protocolo de Ethereum. Cualquier desarrollador puede proponer un nuevo estándar a través de un documento conocido como EIP (Ethereum Improvement Proposal). La comunidad de desarrolladores revisa, debate y, finalmente, decide si la propuesta se acepta como un estándar oficial de ERC.

**Proceso para crear un ERC:**

1. **Propuesta de la idea:** Un desarrollador redacta un EIP describiendo su propuesta. Esto incluye la especificación técnica, el propósito y cómo afectará a la blockchain.
2. **Discusión:** La comunidad de Ethereum revisa y comenta el EIP. Se sugieren mejoras y se discuten posibles problemas o alternativas.
3. **Revisión y aceptación:** Si el EIP pasa por el proceso de revisión con éxito y la comunidad está de acuerdo, se convierte en un ERC oficial.

### Ejemplos de ERC más comunes

1. **ERC-20:** Este es el estándar más conocido y se utiliza para crear tokens fungibles, como criptomonedas. Define funciones como `transfer`, `balanceOf` y `approve` para que los tokens se puedan intercambiar fácilmente entre diferentes aplicaciones.
   * **Usos:** Tokens como DAI, USDT, Pepe.
2. **ERC-721:** El estándar para tokens no fungibles (NFTs). Cada token ERC-721 es único y tiene propiedades específicas, lo que lo hace perfecto para representar activos digitales como arte, coleccionables o bienes raíces virtuales.
   * **Usos:** CryptoKitties, Bored Ape Yacht Club y otros coleccionables digitales.
3. **ERC-1155:** Este estándar combina lo mejor de ambos mundos. Permite la creación de tokens fungibles y no fungibles en el mismo contrato, optimizando el uso de espacio y gas.
   * **Usos:** Juegos y coleccionables como Gods Unchained y Enjin, donde un solo contrato puede gestionar armas, habilidades, personajes y monedas.

### ¿Por qué son importantes los ERC?

1. **Compatibilidad:** Los ERC aseguran que los tokens y contratos inteligentes se comporten de manera predecible, lo que permite que los desarrolladores construyan aplicaciones interoperables sin tener que reinventar la rueda.
2. **Seguridad y confianza:** Al seguir un estándar bien definido y revisado por la comunidad, los desarrolladores pueden evitar errores comunes y fallas de seguridad en sus contratos inteligentes.
3. **Innovación:** Los ERC son una forma de estandarizar nuevas funcionalidades en la blockchain. Permiten a los desarrolladores proponer y adoptar rápidamente nuevas características que beneficien a todo el ecosistema.
