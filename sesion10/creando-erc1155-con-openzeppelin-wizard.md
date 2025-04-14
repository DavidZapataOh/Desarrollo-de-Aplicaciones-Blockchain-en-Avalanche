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

# Creando ERC1155 con Openzeppelin Wizard

Crear un contrato para múltiples tipos de tokens (fungibles y no fungibles) puede ser complicado, pero gracias a **OpenZeppelin Wizard**, puedes configurar y desplegar tu contrato ERC1155 de forma rápida y sencilla, sin necesidad de escribir código desde cero.

### Creando tu ERC1155 con OpenZeppelin Wizard: Paso a Paso

A continuación, te mostramos cómo crear un contrato ERC1155 utilizando esta poderosa herramienta.

**1. Acceder a OpenZeppelin Wizard**

Para comenzar, visita OpenZeppelin Wizard. Encontrarás una interfaz fácil de usar donde puedes configurar varios tipos de contratos, incluyendo ERC20, ERC721 y ERC1155.

**2. Configurar el Token ERC1155**

En la sección **ERC1155** del Wizard, configura los siguientes parámetros:

* **Name**: Especifica el nombre de tu contrato, por ejemplo, "MyToken".
*   **URI**: Define la URI base para todos los tipos de tokens. La URI debe contener `{id}` en el lugar donde se reemplazará automáticamente con el `id` del token. Un ejemplo sería:

    ```arduino
    ipfs://QmZTsFjJGALEVPHcMYGdS1F3xgpAnELUC8KwjijXqXrdNM/1.json
    ```

    Esto permite que cada tipo de token apunte a sus metadatos específicos según su `id`.

**Características adicionales:**

* **Mintable**: Permite la creación de nuevos tokens después del despliegue inicial, lo cual es ideal si planeas añadir diferentes ítems o activos a tu contrato en el futuro.
* **Burnable**: Da a los usuarios la opción de quemar (destruir) sus propios tokens, lo cual reduce el suministro total de esos tokens.
* **Supply Tracking**: Activa el rastreo de suministro, permitiendo consultar la cantidad total de cada tipo de token en circulación.
* **Pausable**: Da la posibilidad de pausar las transferencias en casos de emergencia, añadiendo una capa de seguridad extra.
* **Updatable URI**: Permite modificar la URI base después del despliegue, útil si necesitas actualizar la ubicación de los metadatos.

**3. Generar el Código**

Una vez que hayas configurado todas las opciones según tus necesidades, haz clic en el botón **"Open in Remix"** para abrir el código en Remix IDE, o copia el código generado y pégalo en un archivo dentro de Remix.

**4. Desplegar el Contrato en Remix**

Si optaste por abrir el código en Remix, sigue estos pasos para desplegar tu contrato ERC1155:

* **Conéctate a Remix**: Abre Remix IDE.
* **Cargar el Código**: Copia y pega el código generado en OpenZeppelin Wizard en un nuevo archivo en Remix.
* **Compilar**: Haz clic en el ícono de “compilar” para asegurarte de que el código no tiene errores.
* **Desplegar**: Selecciona “Deploy” y elige la red de Avalanche Testnet (Fuji) o la red que prefieras. Dependiendo de las configuraciones seleccionadas, es posible que debas asignar un propietario o un rol si has habilitado `Access Control`.
* **Verificar**: Usa el plugin de verificación en Remix para verificar el contrato ERC1155, facilitando la transparencia y la validación del código.

**5. Interactuar con tus Tokens**

¡Felicidades! Ahora tienes un contrato ERC1155 desplegado que permite la creación de múltiples tipos de tokens. Puedes interactuar con él desde Remix, mintear diferentes tipos de tokens, quemarlos o gestionar roles de acceso.

### Ejemplo de Minteo de Tokens

Desde Remix, puedes mintear un nuevo token utilizando la función `mint`, pasando como parámetros la dirección del destinatario, el `id` del token y la cantidad deseada.

* **Dirección**: 0x942Fa5b96C52cf4EDE7498e02fbF9196B0510702
* **ID del Token**: 1 (para un tipo específico de token).
* **Cantidad**: 100 (en el caso de un token fungible, puedes establecer cualquier cantidad).

Para crear múltiples tipos de tokens en una sola transacción, utiliza la función `mintBatch`, lo cual es ideal si deseas añadir varios ítems o activos a la vez.
