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

# Creando ERC721 con Openzeppelin Wizard

Crear un token **ERC721** desde cero puede ser un reto, especialmente si eres nuevo en Solidity. Sin embargo, gracias a herramientas como **OpenZeppelin Wizard**, puedes generar contratos ERC721 de manera sencilla y rápida, sin escribir código desde cero.

### ¿Qué es OpenZeppelin Wizard?

**OpenZeppelin Wizard** es una herramienta visual en línea que facilita la creación de contratos inteligentes, permitiéndote elegir las características específicas que deseas incluir en tu contrato. Con esta herramienta, puedes configurar fácilmente todos los aspectos de tu contrato ERC721, como el nombre, el símbolo y características adicionales como minteo seguro y capacidad de quemado, sin preocuparte por los detalles técnicos.

### Creando tu ERC721 con OpenZeppelin Wizard: Paso a Paso

Vamos a ver cómo crear un token ERC721 utilizando esta poderosa herramienta.

**1. Acceder a OpenZeppelin Wizard**

Para comenzar, visita la página de **OpenZeppelin Wizard**. Encontrarás una interfaz amigable donde puedes configurar varios tipos de contratos, incluyendo ERC20, ERC721 (NFTs) y más.

{% embed url="https://wizard.openzeppelin.com/#erc721" %}

**2. Configurar el Token ERC721**

* En la sección **ERC721** del Wizard, puedes configurar los siguientes parámetros:
  * **Nombre del Token**: Establece el nombre de tu colección NFT. Por ejemplo, podrías llamarlo "Membresia".
  * **Símbolo del Token**: Este es el símbolo abreviado que representará a tu colección, como "MEM" para "Membresia".
  * **Base URI**: Configura el URI base que se usará para los metadatos de cada NFT. Esto permite que cada token tenga una URI específica al concatenar el `tokenId` con el URI base que definas.
* **Características adicionales:**
  * **Mintable**: Permite crear (mintear) nuevos NFTs después del despliegue inicial. Ideal si planeas tener una colección que crezca con el tiempo.
  * **Auto Increment IDs**: Automatiza la asignación de IDs incrementales para cada nuevo token mintado, eliminando la necesidad de establecer manualmente el `tokenId` cada vez que se crea un nuevo NFT.
  * **Burnable**: Da a los usuarios la posibilidad de quemar (destruir) sus NFTs, eliminándolos permanentemente de la colección.
  * **Pausable**: Te da la opción de pausar las funciones de transferencia en casos de emergencia.
  * **Ownable**: Define un propietario del contrato con permisos exclusivos, lo cual es útil para controlar la administración de la colección.
  * **Enumerable**: Permite realizar un seguimiento de todos los tokens emitidos. Esto es útil si quieres listar todos los NFTs de la colección o verificar cuántos se han minteado.
  * **URI Storage**: Da la posibilidad de almacenar URIs específicas para cada token, en lugar de depender de un URI base. Esto permite que cada token tenga su propio enlace personalizado a metadatos únicos.

**3. Generar el Código**

Después de configurar todas las opciones a tu gusto, haz clic en el botón de **"Open in Remix"** para abrir el contrato en Remix IDE, o simplemente copia el código generado y pégalo en un archivo dentro de Remix.

**4. Desplegar el Contrato en Remix**

Si has optado por abrir el código en Remix, sigue estos pasos para desplegar tu colección NFT:

* **Conéctate a Remix**: Abre Remix IDE.
* **Cargar el Código**: Copia y pega el código generado en OpenZeppelin Wizard en un nuevo archivo dentro de Remix.
* **Compilar**: Haz clic en el ícono de “compilar” para asegurarte de que el código no tiene errores.
* **Desplegar**: Selecciona “Deploy” y elige la red de Avalanche Testnet (Fuji) o la red de tu preferencia. Dependiendo de las características adicionales que hayas incluido, como `Ownable`, es posible que debas proporcionar una dirección de propietario.
* **Verificar**: Usa el plugin de verificación en Remix para verificar el contrato de tu ERC721.

**5. Interactuar con tu Token NFT**

¡Felicidades! Ahora tienes tu propia colección de NFTs en la blockchain. Puedes interactuar con tu contrato ERC721 directamente desde Remix o, si tienes una wallet compatible con NFTs, podrás ver tus tokens.

### Ejemplo de Minteo de NFT

Desde Remix, puedes mintear un nuevo NFT ejecutando la función `mint`, pasando como parámetro la dirección del destinatario y el `tokenId` único. Con **Auto Increment IDs**, el `tokenId` se asignará automáticamente.

```
// Address
0x942Fa5b96C52cf4EDE7498e02fbF9196B0510702
```

En el caso de un token ERC721, no es necesario manejar decimales como con ERC20, ya que cada token es único e indivisible.

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>
