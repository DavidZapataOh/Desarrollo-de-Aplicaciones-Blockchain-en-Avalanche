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

# Verificar un Contrato

Una vez que has desplegado tu contrato inteligente en la blockchain, el siguiente paso es **verificarlo**. Verificar un contrato es un proceso que permite que cualquier persona pueda ver el código fuente de tu contrato en la blockchain, lo que añade una capa importante de **transparencia**.

### Pasos para verificar un contrato

Verificar un contrato es más fácil de lo que parece. A continuación te explico cómo hacerlo paso a paso:

1.  **Copia la dirección de contrato:** Simplemente copia el address del contrato que desplegaste en Remix.

    <figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>
2.  **Acceder al explorador de bloques**: Dirígete al explorador de bloques de la red donde has desplegado tu contrato. Si es en Avalanche, usa [**SnowScan**](https://snowscan.xyz/)**.** Luego da clic en **Sign In** en la parte superior derecha.

    <figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>
3.  **Crea tu cuenta:** Si aún no tienes cuenta, puedes crear una dando clic en **Sign Up.**

    <figure><img src="../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>
4.  **Ir a la sección de "API Keys"**: Una vez en tu cuenta, busca la opción que dice "API Keys" en el panel izquierdo.

    <figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>
5. **Añade una API**: Ahora, da clic en el botón azul "Add" y asígnale un nombre. Copia el API Key Token, te servirá para verificar los contratos inteligentes en Avalanche de forma sencilla.
6.  **Entra al Plugin Manager**: Después, deberás buscar la extensión "CONTRACT VERIFICATION - ETHERSCAN" en el Plugin Manager de Remix.

    <figure><img src="../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>
7.  **Verificar**: Una vez activado, puedes entrar al plugin mediante el panel izquierdo, lo primero que te va a pedir es el API Key Token, solo debes pegarlo. Ahora, te pedirá que selecciones el contrato y que ingreses el Contract Address que copiaste en el paso 1. Luego dale al botón azul "Verify".

    <figure><img src="../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>
8.  **Confirma la verificación**: Si el proceso de verificación fue exitoso, deberá aparecer el codigo de tu contrato en el verificador.

    * Ingresa al explorador de bloques de Avalanche, en este caso, como desplegamos en Fuji, debemos entrar a la versión testnet del explorador. Puedes [ingresar aquí](https://testnet.snowtrace.io/).
    * Ingresa el address del contrato en el buscador y dale _enter_.
    * Da clic en la pestaña "contract".

    <figure><img src="../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

¡Tu contrato está verificado! Ahora puedes ver como al lado de la pestaña **Code**, hay dos pestañas más, Read Contract y Write Contract, que nos servirá para interactuar con el contrato.
