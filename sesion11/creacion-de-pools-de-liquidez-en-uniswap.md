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

# Creación de Pools de Liquidez en Uniswap

La creación de pools de liquidez en Uniswap permite que los usuarios faciliten intercambios en la plataforma al depositar pares de tokens en un pool. Al hacerlo, actúan como proveedores de liquidez (LP) y reciben una parte de las comisiones generadas por los intercambios en ese pool. Veamos cómo crear un pool tanto en **Uniswap V2** como en **Uniswap V3**.

### Creación de Pools de Liquidez en Uniswap

La creación de pools de liquidez en Uniswap permite que los usuarios faciliten intercambios en la plataforma al depositar pares de tokens en un pool. Al hacerlo, actúan como proveedores de liquidez (LP) y reciben una parte de las comisiones generadas por los intercambios en ese pool. Veamos cómo crear un pool tanto en **Uniswap V2** como en **Uniswap V3**.

#### **Creación de un Pool en Uniswap V2:**&#x20;

1.  **Accede a la Plataforma de Uniswap**: Visita [Uniswap ](https://app.uniswap.org/)y conecta tu wallet (como MetaMask o Core) en la red de Sepolia para interactuar con la plataforma.

    <figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>
2.  **Selecciona “Pool”**: Desde el menú principal, selecciona la pestaña “Pool”, luego abre el menú desplegable “More” y entra en "V2 liquidity".&#x20;

    <figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>
3.  **Añadir liquidez V2**: Da click en "Add V2 liquidity" Esto te permitirá comenzar el proceso de creación de un nuevo pool o unirte a uno existente.

    <figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>
4. **Escoge el Par de Tokens**: Ingresa los dos tokens que deseas depositar en el pool (por ejemplo, **ETH** y **USDC**). Asegúrate de tener suficiente balance de ambos tokens en tu wallet. Incluso, puedes intentar hacerlo con el token que creaste en la sesión "Tokens ERC20".
5.  **Define la Cantidad de Tokens**: Uniswap V2 requiere que deposites cantidades equivalentes de cada token (en términos de valor en dólares) para mantener el equilibrio del pool. Por ejemplo, si deseas depositar 1 ETH, necesitarás agregar la cantidad equivalente en USDC.

    <figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>
6.  **Confirmación y Tarifas de Gas**: Una vez que hayas configurado la cantidad, aprueba la cantidad de tokens que permitirás usar al contrato, luego dale en "Supply" para agregar la liquidez. Esta acción generará una transacción y deberás pagar una tarifa de gas para que el contrato de Uniswap procese la operación.

    <figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>
7. **Recepción de Tokens LP**: Al completar el depósito, recibirás **tokens de liquidez (LP)**, que representan tu participación en el pool. Estos tokens LP te permitirán retirar tu participación y las comisiones ganadas cuando lo desees.

#### **Creación de un Pool en Uniswap V3:**

1. **Accede y Conecta tu Wallet**: Igual que en V2, comienza accediendo a la plataforma de Uniswap y conecta tu wallet.
2.  **Selecciona “Pool”**:  Desde el menú principal, selecciona la pestaña “Pool”, luego entra en "New position".

    &#x20;

    <figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>
3.  **Escoge el Par de Tokens**: En Uniswap V3, selecciona los tokens que deseas agregar al pool (por ejemplo, **AVAX/USDC**).

    <figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>
4.  **Elegir el Nivel de Tarifas**: En Uniswap V3 puedes seleccionar entre diferentes niveles de tarifas (0.01%, 0.05%, 0.3%, y 1%) según el riesgo y la volatilidad del par de tokens. Generalmente, pares más estables como **USDC/USDT** tienen tarifas más bajas, mientras que pares más volátiles, como **ETH/DAI**, pueden tener tarifas más altas.

    <figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>
5.  **Definir el Rango de Precio**: Una de las principales diferencias de V3 es la **liquidez concentrada**. Deberás especificar un rango de precio para cada token en el que deseas que tu liquidez esté activa. Por ejemplo, puedes definir un rango de 15 USDC a 20 USDC para el token AVAX.

    * Este rango permite que tu liquidez sea utilizada solo dentro de los precios seleccionados. Fuera de este rango, tu liquidez quedará inactiva hasta que el precio vuelva a situarse dentro de estos límites.

    <figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>
6.  **Definir la Cantidad de Tokens y Confirmar la Transacción**: Ingresa las cantidades de cada token que deseas aportar al pool y confirma la transacción. Nuevamente, recibirás tokens LP que representan tu participación en el rango de precios especificado.

    <figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>
7. **Administrar el Rango de Precio**: Si el precio se mueve fuera de tu rango, puedes ajustar tu liquidez manualmente o utilizar servicios que la ajusten automáticamente para maximizar tus rendimientos.

### **¿Qué Versión de Uniswap Elegir?**

* **Uniswap V2** es ideal para LP que desean un enfoque más pasivo, sin preocuparse por los cambios de rango de precio. Es una buena opción para quienes prefieren simplicidad.
* **Uniswap V3** es adecuado para LP experimentados que buscan maximizar el rendimiento mediante la liquidez concentrada, aunque requiere una administración más activa.
