---
icon: square-small
---

# Wallets

Ahora ya tenemos un breve contexto sobre cómo interactuamos con la blockchain a través de claves criptográficas, el siguiente paso natural es hablar sobre las wallets. Estas herramientas juegan un papel importantisimo en la gestión y protección de nuestras criptomonedas y activos digitales, actuando como la interfaz entre usuarios y la blockchain. Pero, ¿qué es exactamente una wallet y cómo funciona?

### ¿Qué es una Wallet?

A pesar de su nombre, una wallet (**billetera digital**) no almacena criptomonedas de la misma manera que una biletera física almacena dinero. En lugar de tener los activos directamente, la wallet almacena la clave privada que te permite acceder a tus criptomonedas en la blockchain. Cada vez que realizas una transacción, tu wallet utiliza esta clave para firmar y autorizar el movimiento de los activos.

De hecho, las criptomonedas no se "guardan" en la wallet como tal, sino que residen en la blockchain. Lo que hace la wallet es permitirte acceder a esas criptomonedas asociadas a una **clave pública** mediante el uso de la **clave privada** correspondiente. Es decir, la wallet actúa como un control remoto que te permite gestionar tus fondos que están siempre en la blockchain.

### Tipos de Wallets

Existen varios tipos de wallets, cada una con diferentes niveles de seguridad y accesibilidad, lo que permite a los usuarios elegir la que mejor se adapte a sus necesidades. Estos son los tipos más comunes:

1. **Wallets de Software:** También conocida como **billeteras calientes**, son aplicaciones que instalas en tu computador o celular. Estas wallets son accesibles y convenientes, permitiéndote realizar transacciones desde cualquier lugar donde tengas acceso a internet. Los ejemplos más populares incluyen **MetaMask**, **Trust Wallet** y **Core**.
2. **Wallets de Hardware:** También conocida como **billeteras frías**, son dispositivos físicos, como **Ledger** o **Trezor**, que almacenan las claves privadas de forma offline. Estas son consideradas una de las formas más seguras de almacenamiento de criptomonedas porque mantienen tus claves fuera del alcance de internet, lo que las protege de posibles hackeos.
3. **Wallets de papel:** Es una forma completamente offline de almacenar claves privadas y públicas. Estas son simplemente impresiones físicas que contienen la clave privada y la clave pública en formato alfanumérico o QR. Si se generan correctamente, estas wallets no tienen ninguna conexión digital, lo que las hace inmunes a hackeos en línea.&#x20;
4. **Wallets custodiales:** Es aquella en la que una tercera parte, generalmente una plataforma de intercambio (exchange) como **Binance** o **Coinbase**, almacena tus claves privadas en tu nombre. Esto significa que confías en dicha entidad para custodiar y proteger tus fondos.

### ¿Cómo funcionan las Wallets?

El funcionamiento de una wallet se basa en el uso de **claves criptográficas**. Cuando generas una wallet, se crea un par de **clave privada** y **clave pública**. Como ya explicamos, la clave privada es lo que permite acceder a tus fondos, mientras que la clave pública es como una dirección que puedes compartir para recibir pagos.

Cada vez que envías criptomonedas, la wallet utiliza la clave privada para **firmar** digitalmente la transacción. Este proceso confirma que eres el propietario de los fondos y autoriza su transferencia. Después de la firma, la transacción es transmitida a la red blockchain donde los **nodos** la validan y la registran en el siguiente bloque.

En wallets como **MetaMask** y **Core**, las claves privadas y la frase semilla se gestionan localmente en el dispositivo del usuario, lo que significa que tienes control completo sobre tus fondos, pero también recae en ti la responsabilidad de proteger las claves privadas.

### Abriendo tu Wallet de Core

Core es una plataforma de blockchain desarrollada por **Avalanche**, que permite a los usuarios interactuar con la red Avalanche y otras blockchains compatibles con **EVM** (Ethereum Virtual Machine) de una manera eficiente y segura. Es importante aprendas a cómo obtener y configurar tu wallet de **Core** para que puedas comenzar a interactuar con el ecosistema de Avalanche.

1. **Descarga Core:** Puedes descargar la extensión web o la aplicación oficial de **Core**:

{% embed url="https://chromewebstore.google.com/detail/core-crypto-wallet-nft-ex/agoakfejjabomempkjlepdflaleeobhb" %}

{% embed url="https://core.app/es/?downloadCoreMobile=1" %}

2. **Crear una nueva wallet:** Una vez que hayas instalado la extensión o la aplicación de Core, sigue estos pasos para crear tu wallet:&#x20;
   * Abre la aplicación o la extensión y selecciona la opción **"Crear nueva wallet"**.
   * Core generará una **frase semilla** de 24 palabras para ti. Esta frase es esencial para recuperar tu wallet en caso de que pierdas el acceso a tu dispositivo, así que asegúrate de anotarla en un lugar seguro y no compartirla con nadie.
   * Confirma la frase semilla en el siguiente paso, te pedirá que selecciones algunas palabras en el orden correcto para verificar que la has guardado correctamente.
3. **Configurar tu wallet:** Después de crear tu wallet, Core te pedirá que configures un nombre y una **contraseña**. Esta contraseña es necesaria para acceder a la wallet en tu dispositivo y realizar transacciones.
4. **Conectar con Avalanche y otras redes:** Una vez que hayas configurado tu wallet, estarás listo para interactuar con la **blockchain de Avalanche** y otras redes compatibles con **EVM**. Core se conecta automáticamente a la red principal de Avalanche (Avalanche C-Chain), pero también puedes agregar otras redes manualmente.

### Seguridad en las Wallets

Uno de los aspectos más importantes a considerar al usar wallets es la **seguridad**. Aquí hay algunos puntos clave para garantizar que tus criptomonedas estén siempre protegidas:

* **Nunca compartas tu clave privada o frase semilla**: La clave privada es la única forma de acceder a tus fondos. Si alguien obtiene tu clave privada o frase semilla, puede robar todas tus criptomonedas sin que tengas posibilidad de recuperarlas.
* **Utiliza contraseñas fuertes y autentificación de dos factores (2FA)**: Si usas una wallet de software (caliente) o custodial, siempre habilita medidas de seguridad adicionales como 2FA para proteger tu cuenta.
* **Haz respaldos regulares de tu frase semilla**: Guarda la frase semilla en un lugar seguro, preferiblemente offline, como una hoja de papel o un dispositivo de almacenamiento en frío.
