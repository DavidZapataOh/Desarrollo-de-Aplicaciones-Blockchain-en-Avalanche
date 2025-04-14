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

# Pragma

El `pragma` es una directiva que le dice al compilador de Solidity qué versión de Solidity debe usar para compilar el contrato. En otras palabras, es como una "regla" que establece el rango de versiones del compilador en las que tu código puede ser ejecutado de manera segura. Esto es importante porque diferentes versiones de Solidity pueden tener cambios significativos en su sintaxis o comportamiento, y especificar la versión correcta asegura que tu contrato funcione como lo planeaste.

El pragma suele ir debajo de la licencia y su formato más común es:

```solidity
pragma solidity ^0.8.18;
```

Esta línea le está diciendo al compilador que puede usar cualquier versión de Solidity desde la 0.8.18 en adelante, pero no mayor a la siguiente versión importante, como la 0.9.0. Esto permite que tu código se mantenga compatible con futuras actualizaciones menores, sin romperse por cambios importantes.

También hay otras maneras de especificar la versión del compilador, aunque no sueles ser tan comunes:

*   **Versión fija**: Si deseas que tu contrato solo sea compilado con una versión exacta de Solidity, puedes especificar una versión fija, como en este ejemplo:

    ```solidity
    pragma solidity 0.8.7;
    ```

    Esto significa que tu contrato solo se podrá compilar con la versión 0.8.7 de Solidity. Si intentas compilarlo con una versión diferente, el compilador arrojará un error.
*   **Versión con rango**: En lugar de usar una versión fija, puedes permitir que el contrato se compile con un rango de versiones, lo que te da más flexibilidad:

    ```solidity
    pragma solidity >=0.7.0 <0.9.0;
    ```

    Este pragma indica que tu contrato puede ser compilado con cualquier versión de Solidity desde la 0.7.0 hasta cualquier versión menor a la 0.9.0. De esta forma, tu código se mantiene compatible con una gama más amplia de versiones del compilador.



En nuestro caso. definiremos el pragma de la manera clásica, y en la versión 0.8.20 o superior.

<figure><img src="../.gitbook/assets/image (86).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Si recibes un error acá, probablemente sea porque la versión de compilador que tienes configurado en Remix sea diferente a la que declaraste en el `pragma`. Más adelante veremos como solucionar este error.
{% endhint %}
