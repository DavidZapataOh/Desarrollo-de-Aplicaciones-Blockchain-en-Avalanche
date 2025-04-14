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

# Seguimiento de una Transacción

Ahora que entendemos cómo interactuamos con la blockchain mediante claves criptográficas y wallets, es momento de explorar **qué sucede cuando realizamos una transacción** y cómo podemos seguir cada paso del proceso en la red de **Avalanche**.

Aquí es donde entran en juego los **exploradores de bloques**. Imagina estos exploradores como ventanas que nos permiten ver dentro de la blockchain. Por ejemplo, si usamos Bitcoin tenemos **Blockchain.info,** para Ethereum está **Etherscan,** y en el caso de **Avalanche** contamos con **SnowTrace**.

Imagina que quieres enviar **AVAX**, la criptomoneda nativa de Avalanche, a un amigo. Desde el momento en que decides hacer esta transacción hasta que se confirma en la blockchain, ocurren varios pasos interesantes que vale la pena conocer.

### Paso 1: Iniciando la transacción desde tu Wallet

Todo comienza cuando abres tu wallet, por ejemplo, **Core** o **MetaMask**, y decides enviar una cantidad específica de AVAX a la dirección de tu amigo. Ingresas la dirección del destinatario, el monto a enviar y ajustas las configuraciones de la transacción si es necesario, como las tarifas de gas.

Al presionar el botón de **"Enviar"**, tu wallet crea una **transacción** que incluye:

* **Tu dirección pública** (remitente).
* **La dirección pública de tu amigo** (destinatario).
* **El monto** de AVAX que deseas transferir.
* **Información adicional**, como las tarifas de transacción y un **nonce**, que es un número que garantiza que cada transacción sea única.

### Paso 2: Firmando la transacción con tu clave privada

Antes de que la transacción pueda ser enviada a la red, necesita ser **firmada digitalmente**. Tu wallet utiliza tu **clave privada** para generar una firma criptográfica única. Esta firma garantiza que la transacción fue autorizada por ti y que no ha sido alterada en el camino.

Es importante destacar que tu clave privada nunca se envía a la red, solo la firma resultante, lo que mantiene tu información segura.

### Paso 3: Transmisión de la transacción a la red de Avalanche

Una vez firmada, tu wallet envía la transacción a la red de **Avalanche**. Aquí es donde los **nodos** entran en acción. Los nodos son computadoras que mantienen una copia de la blockchain y validan las transacciones que reciben.

### Paso 4: Validación de la transacción por los nodos

Los nodos de Avalanche utilizan el **mecanismo de consenso** de **Avalanche Consensus**, que es conocido por su alta velocidad y eficiencia. Este proceso implica:

* **Muestreo aleatorio**: Cada nodo selecciona un pequeño subconjunto aleatorio de otros nodos para consultar sobre la validez de la transacción.
* **Metastabilidad**: A través de múltiples rondas de consulta, los nodos rápidamente llegan a un acuerdo sobre si la transacción es válida o no.

Durante este proceso, los nodos verifican que:

* La firma de la transacción es válida y coincide con la dirección del remitente.
* El remitente tiene suficientes fondos para cubrir el monto de la transacción y las tarifas.
* No hay intentos de doble gasto, es decir, que los mismos fondos no se estén utilizando en otra transacción simultáneamente.

### Paso 5: Inclusión de la transacción en un bloque

Una vez que la transacción es validada se incluye en un **bloque** junto con otras transacciones. Debido a la eficiencia del mecanismo de consenso de Avalanche este proceso ocurre en menos de un segundo.

### Paso 6: Confirmación de la transacción

Después de que el bloque es agregado a la blockchain, la transacción se considera **confirmada**. En Avalanche las transacciones suelen alcanzar la finalización prácticamente instantánea, lo que significa que no necesitas esperar largos períodos para que tu transacción sea irrevocable.

### Paso 7: Verificación de la transacción en SnowTrace

Para asegurarte de que todo ha salido bien, puedes verificar tu transacción en el explorador de bloques **SnowTrace**. Sigue estos pasos:

1. **Obtener el hash de la transacción**: Tu wallet te proporcionará el **hash** o identificador único de la transacción una vez que se haya enviado. En este caso seguiremos una transacción que yo hice enviando 1 AVAX a otra dirección, este fue el hash generado:

```
0x2de74e0c605005295d8abef6ce2e7f37f2c39106183e8d3b07665dfb7d1bdab6
```

2. Acceder a SnowTrace: En este caso accederemos a la testnet, donde se realizan pruebas sin tener que gastar dinero real.

{% embed url="https://testnet.snowtrace.io/" %}

3. **Ingresar el hash en el buscador**: Pega el hash de la transacción que te di en el paso 1 en la barra de búsqueda y presiona _Enter_.
4.  **Revisar los detalles de la transacción**:

    * **Blockchain:** Debería aparecer **Fuji** (red de prueba de Avalanche)
    * **Estado de la transacción**: Debería aparecer como **Success**.
    * **Bloque**: Número del bloque en el que se incluyó tu transacción.
    * **Tiempo de inclusión (timestamp)**: Verás la marca de tiempo que indica cuándo se procesó.
    * **Direcciones**: Las direcciones del remitente y destinatario.
    * **Monto y tarifas**: El monto enviado (1.00 AVAX) y las tarifas pagadas (Fee).

    <figure><img src="../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

Esta transparencia es uno de los pilares fundamentales de la tecnología blockchain. Todos podemos verificar nuestras transacciones sin necesidad de intermediarios o entidades centralizadas. Además aumentamos nuestra confianza en el sistema y en las operaciones que realizamos.

Sin embargo es importante mencionar que, aunque las transacciones son públicas, nuestras identidades permanecen anónimas. La blockchain muestra direcciones y montos, pero no revela información personal, manteniendo así nuestra privacidad.
