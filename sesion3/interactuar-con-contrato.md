---
icon: square-small
---

# Interactuar con Contrato

Una vez que tu contrato ha sido desplegado y verificado, ya puedes **interactuar con él**. Interactuar con un contrato inteligente significa usar sus funciones, ya sea para leer información o para realizar acciones en la blockchain. Hay dos formas principales de interactuar con un contrato, directamente desde **Remix** o usando un **explorador de bloques** como **Snowtrace**.

### Interactuar con un contrato desde Remix

Remix no solo es útil para desarrollar y desplegar contratos, también te permite interactuar con ellos una vez que están desplegados. Aquí te explico cómo hacerlo:

1. **Sección de despliegue**: Si ya tienes tu contrato desplegado, ve a la pestaña de **"Deploy & Run Transactions"** en Remix.
2.  **Seleccionar el contrato desplegado**: En la sección de **Deployed Contracts** de Remix, verás una lista de contratos que has desplegado. Cada contrato tendrá su propia sección desplegable donde puedes ver las funciones que están disponibles.



    <figure><img src="../.gitbook/assets/image (95).png" alt=""><figcaption></figcaption></figure>
3.  **Ejecutar funciones**: Simplemente haz clic en las funciones que deseas ejecutar. Si la función es de solo lectura (como `leerMensaje`), se ejecutará sin costo. Pero si la función modifica el estado de la blockchain (por ejemplo, si envías fondos o cambias una variable, cómo en el caso de `enviarMensaje`), necesitarás pagar **gas** para procesar la transacción. En este caso, Remix te pedirá que confirmes la transacción. En nuestro caso primero ejecutaremos `enviarMensaje`, ingresando como parámetro el texto que quieras. Una vez se confirme la transacción, ejecuta `leerMensaje`, y verás que la variable almacenó el valor correctamente.



    <figure><img src="../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Si obtienes algun error a la hora de ejecutar la función `leerMensaje`, puedes estar teniendo problemas de compatibilidad con la versión de la EVM. Para solucionarlo, ve a la configuración avanzada de compilador y cambia la EVM VERSION a **shanghai**. Luego, vuelve a desplegar el contrato.
{% endhint %}

### Interactuar con un contrato desde un explorador de bloques

Si prefieres interactuar con tu contrato directamente desde un **explorador de bloques** como **Snowtrace**, también es posible y muy útil, especialmente si tu contrato ya está en una red pública y deseas que otros usuarios puedan interactuar con él sin tener que usar Remix.

1. **Acceder al explorador de bloques**: Ve al explorador de bloques de [**Snowtrace** ](https://testnet.snowtrace.io/)en la versión de prueba (Fuji).
2.  **Buscar la dirección del contrato**: Usa la dirección del contrato para buscarlo en el explorador de bloques. Una vez que lo encuentres, verás una pestaña llamada **"Contract"** donde puedes ver su información.



    <figure><img src="../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>
3.  **Ir a "Write Contract" o "Read Contract"**: Dependiendo de lo que quieras hacer, puedes ir a la pestaña de **"Read Contract"** para ver los datos almacenados (por ejemplo, balances o estados), o a **"Write Contract"** si deseas ejecutar una función que modifique el estado del contrato (como transferir tokens, enviar fondos o interactuar con una dApp).

    \[**Imagen**: Pantalla de Etherscan mostrando las pestañas de "Read Contract" y "Write Contract".]
4. **Conectar tu wallet**: Si quieres ejecutar una función que implique cambios en la blockchain, necesitarás conectar tu wallet de Core para firmar y enviar la transacción. Esto se hace directamente desde el explorador de bloques.
5.  **Ejecutar funciones**: Al igual que en Remix, puedes ejecutar las funciones disponibles en el contrato. Solo recuerda que las funciones que modifican la blockchain requerirán pagar tarifas de gas.<br>

    <figure><img src="../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>
