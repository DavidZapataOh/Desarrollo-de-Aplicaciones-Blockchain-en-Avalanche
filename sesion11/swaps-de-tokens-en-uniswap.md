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

# Swaps de tokens en Uniswap

El **swap de tokens** es una de las funciones principales de Uniswap, permitiendo a los usuarios intercambiar un token por otro de manera descentralizada y sin intermediarios. Este mecanismo es clave para el funcionamiento de Uniswap, ya que facilita los intercambios de manera rápida, segura y accesible para cualquier usuario, sin importar su experiencia en el mercado de criptomonedas.

### **¿Qué es un Swap de Tokens?**

El swap en Uniswap permite a los usuarios intercambiar un token ERC-20 por otro utilizando los pools de liquidez. Cada swap sigue la fórmula de producto constante **(x \* y = k)** para determinar el precio del intercambio, ajustando el valor de los tokens en función de la oferta y demanda dentro del pool.

Un swap se realiza a través de un **contrato inteligente**, donde el usuario envía una cantidad de tokens A al contrato y recibe a cambio una cantidad de tokens B, basada en el ratio actual en el pool y teniendo en cuenta la comisión de intercambio.

### **Realizar un Swap de Tokens en Uniswap**

1. **Accede a la Plataforma de Uniswap**: Visita Uniswap y conecta tu wallet (MetaMask o Core) para interactuar con la plataforma.
2. **Selecciona la Función de Swap**: En la página principal de Uniswap, o selecciona la pestaña de “Swap”, donde podrás elegir los tokens que deseas intercambiar.
3.  **Escoge los Tokens**: Selecciona el token que quieres intercambiar (por ejemplo, **ETH**) y el token que deseas recibir (por ejemplo, **USDC**). Asegúrate de tener suficiente balance del token inicial en tu wallet.

    <figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>
4. **Define la Cantidad y Revisa la Tolerancia al Deslizamiento**: Ingresa la cantidad que deseas intercambiar y revisa el slippage tolerance (haciendo clic en el engranaje), que es la variación de precio aceptable durante la transacción. Esto es especialmente importante en mercados volátiles, ya que protege al usuario de recibir menos de lo esperado si el precio cambia.
5.  **Confirma el Swap**: Revisa los detalles del intercambio, incluidas las tarifas de gas, y confirma la transacción en tu wallet. Una vez confirmada, el contrato inteligente de Uniswap realiza el intercambio de tokens utilizando el pool de liquidez.

    <figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>
6. **Recibe los Tokens en tu Wallet**: Una vez procesada la transacción, recibirás los tokens directamente en tu wallet. Puedes verificar la transacción en Etherscan para asegurarte de que se haya completado correctamente.
