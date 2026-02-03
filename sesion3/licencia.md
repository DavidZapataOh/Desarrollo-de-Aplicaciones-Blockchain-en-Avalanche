---
icon: square-small
---

# Licencia

El primer recibimiento cuando creas un archivo `.sol` es una advertencia:

<figure><img src="../.gitbook/assets/image (82).png" alt=""><figcaption></figcaption></figure>

Esto es debido a que Solidity te pide que en la primera linea de codigo debes declarar el tipo de licencia del archivo. Al especificar una licencia, le dices a la comunidad qué pueden hacer con tu contrato, si pueden modificarlo, distribuirlo o usarlo en sus propios proyectos.

En otras palabras, la licencia define los términos bajo los cuales tu código puede ser compartido o reutilizado por otros desarrolladores.

### Tipos de licencias comunes en Solidity

Al escribir contratos en Solidity, lo más común es usar una licencia **open source**, lo que permite que otros desarrolladores usen, modifiquen y mejoren tu código. Algunas de las licencias más utilizadas en el mundo de los contratos inteligentes son:

1.  **MIT License**: Esta es una de las licencias más comunes y permisivas. Básicamente permite que cualquiera use, copie, modifique y distribuya tu código, siempre que incluyan una copia del aviso de derechos de autor original. Es ideal si quieres que tu código sea completamente abierto.

    ```solidity
    // SPDX-License-Identifier: MIT
    ```
2.  **GPL-3.0 License**: Esta licencia es más restrictiva que la MIT. Permite que otros usen y modifiquen tu código, pero cualquier derivación de tu trabajo debe mantener la misma licencia. Esto asegura que el código modificado también sea open source.

    ```solidity
    // SPDX-License-Identifier: GPL-3.0
    ```
3.  **Unlicense**: Si prefieres que tu código no tenga restricciones y sea completamente público, puedes usar la **Unlicense**, que permite a cualquiera hacer lo que quiera con tu código, sin obligaciones.

    ```solidity
    // SPDX-License-Identifier: Unlicense
    ```



Para el código que estamos desarrollando usaremos la licencia MIT, por lo cual, agregaremos ese código en la primera linea.

<figure><img src="../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>
