---
icon: square-small
---

# Desplegar un Contrato en la Testnet

Ya tienes tu contrato inteligente escrito y compilado. Ahora viene la parte emocionante, **desplegarlo en la blockchain**. Cuando hablamos de "desplegar" un contrato, nos referimos al proceso de subir tu contrato a la blockchain para que esté disponible de manera pública y cualquiera pueda interactuar con él.

Ya no puedes cambiar el código una vez que el contrato está desplegado, así que es fundamental asegurarse de que todo funcione correctamente antes de dar este paso.

Además, cada despliegue de un contrato requiere una **transacción** en la blockchain, lo que significa que vas a necesitar pagar **gas fees** (tarifas de transacción) con la criptomoneda de la red que estés usando, como **ETH** en Ethereum o **AVAX** en Avalanche.

### Cómo desplegar un contrato en Remix

Aquí te dejo los pasos para desplegar un contrato utilizando **Remix**:

1.  **Seleccionar la pestaña de "Deploy & Run Transactions"**: En la barra lateral izquierda de Remix, haz clic en el icono de la pestaña que dice **Deploy & Run Transactions**. Esta sección te permitirá configurar cómo y dónde quieres desplegar tu contrato.



    <figure><img src="../.gitbook/assets/image (29) (1).png" alt=""><figcaption></figcaption></figure>
2.  **Ten lista tu wallet**: Si planeas desplegar tu contrato en una red real (ya sea una **Testnet** o la **mainnet**), necesitas conectar una wallet, en este caso **Core**. Asegúrate de tener la wallet configurada y lista, y que esté conectada a la red en la que deseas desplegar tu contrato, en este caso la testnet de Avalanche.



    <figure><img src="../.gitbook/assets/image (30) (1).png" alt=""><figcaption></figcaption></figure>
3.  **Elegir el entorno (Environment)**: Remix te permite elegir entre diferentes redes para desplegar tu contrato. Las opciones más comunes son:

    * **Remix VM**: Es una simulación local. Solo se usa para pruebas dentro de Remix y no implica costos ni despliega el contrato en una blockchain real.
    * **WalletConnect**: Esta opción se usa cuando estás conectando tu wallet, como **Core**, para desplegar en **Avalanche**.



    <figure><img src="../.gitbook/assets/image (31) (1).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../.gitbook/assets/image (34) (1).png" alt=""><figcaption></figcaption></figure>

    Es probable que te salga un mensaje diciendo que la app no soporta la red selecciona, pero esto se trata de un error, simplemente dale a la "X" que está en la parte superior derecha.

    <figure><img src="../.gitbook/assets/image (35) (1).png" alt=""><figcaption></figcaption></figure>
4. **Seleccionar el contrato**: En la misma sección de **Deploy & Run Transactions**, verás un menú donde puedes elegir cuál de tus contratos quieres desplegar (en caso de que tengas más de uno en tu proyecto). En nuestro caso, solo tenemos uno.
5.  **Desplegar el contrato**: Una vez que hayas seleccionado tu red y el contrato, solo necesitas hacer clic en el botón naranja que dice **"Deploy"**. Esto generará una transacción en la blockchain. Si estás conectado a Avalanche, verás que tu wallet te pedirá confirmar la transacción y te mostrará las **tarifas de gas** que debes pagar.



    <figure><img src="../.gitbook/assets/image (36) (1).png" alt=""><figcaption></figcaption></figure>
6.  **Verificar el despliegue**: Cuando la transacción sea confirmada, tu contrato estará desplegado en la blockchain. En Remix verás una nueva sección que te permitirá interactuar con el contrato directamente. También recibirás la **dirección** del contrato, que es esencialmente su "ubicación" en la blockchain. Con esa dirección cualquiera puede interactuar con tu contrato.



    <figure><img src="../.gitbook/assets/image (37) (1).png" alt=""><figcaption></figcaption></figure>

