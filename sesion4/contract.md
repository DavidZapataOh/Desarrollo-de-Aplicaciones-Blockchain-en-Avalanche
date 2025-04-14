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

# Contract

¡Ya no tenemos advertencias! Ahora si podemos seguir con la declaración de los contratos. Cuando estamos trabajando con **Solidity**, los **contratos** son el núcleo de todo. Cada contrato inteligente que creamos es básicamente un conjunto de funciones y datos que pueden ser almacenados y ejecutados en la blockchain.

Cada vez que creas un contrato, lo que estás haciendo es definir las reglas y las acciones que se pueden tomar cuando alguien interactúa con ese contrato en la blockchain.

La declaración de un contrato en Solidity es bastante simple. Usamos la palabra clave `contract` seguida del nombre que quieras darle a tu contrato, como por ejemplo:

```solidity
contract MiPrimerContrato {
    // Aquí va todo el código del contrato
}
```

Esta es la estructura básica para crear cualquier contrato en Solidity. Dentro de este bloque es donde definirás todas las funciones, variables y eventos que forman parte de tu contrato inteligente.

Como puedes observar se usa la convención PascalCase a la hora de declarar el nombre del contrato, es decir, la primera letra de cada una de las palabras es mayúscula. Ejemplo: _EjemploDePascalCase_.

Los contratos en Solidity son similares a las clases en los lenguajes orientados a objetos. Cada contrato puede contener declaraciones de Variables de Estado, Funciones, Modificadores, Eventos, Errores, Tipos Struct y Tipos Enum. Además, los contratos pueden heredar de otros contratos.

<figure><img src="../.gitbook/assets/image (87).png" alt=""><figcaption></figcaption></figure>
