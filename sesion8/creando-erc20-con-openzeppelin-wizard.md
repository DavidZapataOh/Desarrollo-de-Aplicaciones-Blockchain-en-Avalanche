---
icon: square-small
---

# Creando ERC20 con Openzeppelin Wizard

Crear un token ERC20 desde cero puede ser un poco enredado, especialmente si eres nuevo en Solidity. Pero gracias a herramientas como OpenZeppelin Wizard, ahora puedes generar contratos ERC20 con solo unos pocos clics, sin necesidad de escribir una sola línea de código.

### ¿Qué es OpenZeppelin Wizard?

OpenZeppelin Wizard es una herramienta visual en línea que te permite crear contratos inteligentes de manera rápida y sencilla, seleccionando las características que deseas incluir. Con esta herramienta puedes configurar todo lo necesario para tu contrato ERC20, desde el nombre y símbolo del token hasta funciones adicionales como minteo, quemado, o snapshots, sin preocuparte por los detalles técnicos.

### Creando tu ERC20 con OpenZeppelin Wizard: Paso a Paso

Vamos a ver cómo crear un token ERC20 utilizando esta increíble herramienta.

**1. Acceder a OpenZeppelin Wizard**

Lo primero que debes hacer es ir a la página de OpenZeppelin Wizard. Aquí verás una interfaz amigable que te permite configurar varios tipos de contratos, incluyendo ERC20, ERC721 (NFTs) y más.

{% embed url="https://wizard.openzeppelin.com/" %}

**2. Configurar el Token ERC20**

* **Selecciona el tipo de contrato:** En la sección de ERC20, puedes configurar los siguientes parámetros:
  * **Nombre del Token:** Elige el nombre que tendrá tu token, yo le pondré “Genesis”.
  * **Símbolo del Token:** Este es el símbolo que representará tu token, en mi caso “GNS”. Es cómo el FCB del FC Barcelona, o el COL de Colombia.
  * **Premint:** La cantidad de tokens que se crearán al desplegar el contrato. Por ejemplo, puedes establecerlo en 1,000,000.
* **Características adicionales:**
  * **Mintable:** Permite crear más tokens después del despliegue inicial. Ideal si quieres tener la capacidad de aumentar la cantidad de tokens en circulación.
  * **Burnable:** Los usuarios pueden quemar (destruir) sus propios tokens, reduciendo la cantidad total en circulación.
  * **Pausable:** Te da la opción de pausar las funciones de transferencia en casos de emergencia.
  * Ownable: Es ideal para controlar el acceso a funciones específicas, definiendo un propietario del contrato que puede transferir la propiedad a otro usuario.

<figure><img src="../.gitbook/assets/image (63) (1).png" alt=""><figcaption></figcaption></figure>

**3. Generar el Código**

Una vez que hayas configurado todas las opciones según tus necesidades, haz clic en el botón de "Open in Remix" o simplemente cópialo y pégalo.&#x20;

**4. Desplegar el Contrato en Remix**

Si has elegido la opción de abrir el código en Remix, sigue estos pasos para desplegar tu token:

1. **Conéctate a Remix:** Ve a [Remix IDE](https://remix.ethereum.org/).
2. **Cargar el Código:** Copia y pega el código generado en OpenZeppelin Wizard en un nuevo archivo dentro de Remix.
3. **Compilar:** Haz clic en el ícono de “compilar” para asegurarte de que el código no tiene errores.
4. **Desplegar:** Selecciona “Deploy” y elige la red de Avalanche Testnet (Fuji). Según las características adicionales que añadas, te pedirá que ingreses valores como parámetros, en mi caso, al añadir Ownable, me pedirá la dirección que será dueña del contrato.
5. **Verificar:** Usa el plugin de verificación para verificar el contrato de tu ERC20,
6. **Wallet:** Al abrir tu wallet de Core, verás reflejados automáticamente tus tokens.

<figure><img src="../.gitbook/assets/image (64) (1).png" alt=""><figcaption></figcaption></figure>

**5. Interactuar con tu Token**

¡Felicidades! Ahora tienes tu propio token ERC20 desplegado. Puedes interactuar con él directamente desde Remix o usar Core para enviar, recibir y ver tus tokens.

¡Intenta enviarme un poco de tus tokens! Ve a Remix y ve a la sección de contratos desplegados, ahora, ejectuta la función `transfer` , pasando como parámetro el address del destinatario (0x942Fa5b96C52cf4EDE7498e02fbF9196B0510702), y la cantidad de tokens que quieras enviar, recuerda tener en cuenta el numero de decimales que has definido, si vas a mandar 50 tokens, debes ingresar 50 \* 10^`decimals`. En mi caso yo dejé el valor por defecto (18), por lo cual debería ingresar 50 \* 10^18.

```
// Address
0x942Fa5b96C52cf4EDE7498e02fbF9196B0510702
// Cantidad a transferir (50 * 10^18)
50000000000000000000
```

<figure><img src="../.gitbook/assets/image (65) (1).png" alt=""><figcaption></figcaption></figure>

### Ventajas de Usar OpenZeppelin Wizard

1. **Simplicidad:** No necesitas ser un experto en Solidity para crear un token funcional y seguro. OpenZeppelin Wizard se encarga de la parte difícil.
2. **Seguridad:** Los contratos generados siguen los estándares de OpenZeppelin, lo que asegura que sean seguros y estén alineados con las mejores prácticas de la industria.
3. **Personalización:** Puedes elegir exactamente qué características quieres en tu token, asegurando que se adapte a las necesidades de tu proyecto sin añadir complejidad innecesaria.
