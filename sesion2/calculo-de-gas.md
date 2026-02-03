---
icon: square-small
---

# Cálculo de Gas

Es hora de abordar otro tema clave en blockchain, el **cálculo de gas**. Si alguna vez has realizado una transacción o interactuado con un contrato inteligente, seguramente te has topado con el concepto de **gas**. Aunque pueda parecer confuso al principio, el gas es una parte fundamental del funcionamiento de la red.

### GAS

En términos simples, el **gas** es la unidad que mide la cantidad de trabajo computacional que se necesita para ejecutar operaciones. Cada vez que haces algo en la red, ya sea enviar criptomonedas, interactuar con un contrato inteligente o participar en una dApp, estás utilizando el poder computacional de los nodos que validan y procesan tu transacción. Es como poner **gas**olina en un auto, sin el gas la transacción no se puede mover.

Pero no todas las transacciones son iguales. Algunas requieren más **gas** que otras, dependiendo de la complejidad de lo que estás intentando hacer. Enviar ETH a un amigo puede ser relativamente barato, pero interactuar con un contrato inteligente complejo, como un proyecto DeFi o un mercado de NFTs, podría requerir mucho más gas.

### ¿Cómo se calcula?

El gas funciona de manera similar a cómo funcionan las tarifas en otros servicios. El costo de una transacción, al menos en Ethereum, se determina por dos cosas:

1. **Gas necesario (Gas Limit)**: Esta es la cantidad de gas que necesitas para ejecutar una operación específica. Cada tipo de transacción o contrato inteligente tiene un costo diferente en gas. Por ejemplo, enviar ETH de una cuenta a otra puede costar 21,000 unidades de gas, mientras que interactuar con un contrato inteligente complejo puede requerir mucho más.
2. **Precio del gas (Gas Price)**: Esto es lo que estás dispuesto a pagar por cada unidad de gas. El precio del gas se mide en **gwei**, una pequeña fracción de ETH. Cuanto mayor sea el precio del gas que estés dispuesto a pagar, más rápida será tu transacción, porque los validadores priorizan las transacciones con tarifas más altas.

El costo total de una transacción se calcula multiplicando estas dos cosas:

```
Costo total de la transacción = Gas Limit * Precio del gas
```

### ¿Por qué varía el precio del gas?

El **precio del gas** no es constante. Funciona en base a la oferta y la demanda de la red. Cuando hay mucha gente usando Ethereum (como cuando se lanzan nuevos proyectos con mucha expectativa o cuando el mercado DeFi está muy activo), el precio del gas tiende a subir. Esto ocurre porque los usuarios están compitiendo por espacio en los bloques para que sus transacciones sean procesadas más rápido.

Durante momentos de alta congestión, el precio del gas puede dispararse. Algunos usuarios están dispuestos a pagar más para que sus transacciones se procesen antes, lo que puede hacer que las tarifas se vuelvan muy altas, especialmente para aquellos que no tienen prisa.

Por otro lado, cuando la red está más tranquila el precio del gas baja, haciendo que las transacciones sean más baratas.

### ¿Cómo afecta esto a los usuarios?

Cuando ejecutas una transacción en Ethereum, debes especificar un **Gas Limit** (límite de gas). Este límite define la cantidad máxima de gas que estás dispuesto a gastar en la transacción. Si la transacción requiere más gas del que has especificado, la operación falla, pero igual pierdes el gas gastado hasta ese punto.

Si por el contrario estableces un Gas Limit demasiado alto, solo se te cobrará el gas que realmente utilices. Pero establecerlo demasiado bajo puede hacer que la transacción quede atascada o falle.

Para los usuarios esto significa que siempre debes ser consciente de cuánta gas estás dispuesto a pagar y ajustar el precio del gas según la urgencia de tu transacción. Afortunadamente, wallets como **Core** y **MetaMask** calculan automáticamente el Gas Limit para la mayoría de las transacciones, y te permiten elegir entre diferentes opciones de precios de gas dependiendo de si prefieres que tu transacción sea **rápida**, **estándar** o **lenta**.
