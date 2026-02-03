---
icon: square-small
---

# Interacción con la Blockchain

Otro aspecto fundamental para entender cómo nos relacionamos con la blockchain es la **interacción mediante claves criptográficas**, específicamente las **claves públicas y privadas** que mencionamos anteriormente. Estas claves son esenciales para realizar transacciones y garantizar la seguridad y autenticidad en la red.

La **criptografía asimétrica** es el corazón de este proceso. Se basa en la generación de un par de claves. La clave privada es como la llave de tu caja fuerte digital, mientras que la clave pública es como tu dirección postal a la que otros pueden enviarte información o, en este caso criptomonedas.

### Bits y Bytes

Antes de profundizar, es importante entender qué son los **bits** y los **bytes** y su diferencia. Un **bit** es la unidad más pequeña de información en computación y puede tener un valor de **0** o **1**. Un **byte** está compuesto por **8 bits** y es una unidad comúnmente utilizada para representar cantidades mayores de datos. Por ejemplo, un carácter en texto ASCII generalmente ocupa 1 byte (8 bits).

Cuando hablamos de una clave privada de **256 bits**, nos referimos a una secuencia de 256 dígitos binarios (ceros y unos). Esto equivale a **32 bytes** (256 bits ÷ 8 bits por byte).

### Entropía en la generación de claves

La **entropía** es un concepto clave en criptografía y se refiere al grado de aleatoriedad o incertidumbre en la generación de claves. Cuanta más entropía tenga un sistema, más impredecible será, lo que incrementa la seguridad.

Al generar una clave privada en blockchain se utiliza una cantidad suficiente de entropía para asegurar que cada clave generada sea única. Por eso es crucial que las herramientas que uses para generar claves sean de confianza y capaces de producir suficiente entropía para evitar vulnerabilidades.

### Generación de Claves en Bitcoin

En Bitcoin las claves se generan utilizando algoritmos criptográficos basados en **criptografía de curva elíptica** (ECC), específicamente la curva **secp256k1**. Este proceso implica generar un número aleatorio de 256 bits (32 bytes), que se convierte en tu clave privada. A partir de esta clave privada se calcula la clave pública mediante operaciones matemáticas en la curva elíptica.

La clave pública resultante es una secuencia más larga. En Bitcoin las direcciones se derivan de la clave pública aplicando funciones hash (SHA-256 y RIPEMD-160) y una codificación especial llamada Base58Check, que produce una dirección más corta y manejable.

Para tener una experiencia práctica puedes utilizar herramientas en línea que permiten generar estos pares de claves para fines educativos. Por ejemplo la página web [**bitaddress.org**](https://www.bitaddress.org) es una herramienta de código abierto que puedes usar para generar claves privadas y públicas de Bitcoin sin necesidad de instalar una wallet. Sin embargo, es importante recordar que por seguridad nunca debes usar claves privadas generadas en línea para manejar fondos reales.

```
// Ejemplo de clave privada:
L4jzJwZvVgxfWWN2izdpJMS8VhBaEQohG3tNjPGFDVyQfoS8tXwA

// Ejemplo de Bitcoin Address:
1CKNwh13y792L3Lebntu3R1GUrGFqcDRRG
```

### Generación de Claves en Ethereum

En **Ethereum**, y en redes compatibles como Avalanche, el proceso es similar pero con algunas diferencias clave. Ethereum también utiliza criptografía de curva elíptica con la misma curva **secp256k1**. La clave privada es un número aleatorio de 256 bits (32 bytes, 64 caracteres hexadecimales). A partir de esta clave privada, se genera la clave pública, que es una secuencia de **128 caracteres** hexadecimales (512 bits o 64 bytes), que incluye las coordenadas **X** e **Y** de la curva elíptica.

Sin embargo, para hacer el proceso más eficiente, **Ethereum comprime la clave pública**. En lugar de almacenar ambas coordenadas (**X** e **Y**), solo se almacena la coordenada **X**, junto con un bit adicional que permite calcular **Y**. Esta compresión reduce la clave pública a **66 caracteres** hexadecimales (33 bytes), lo que hace que el manejo de las claves sea más eficiente sin comprometer la seguridad.

Para obtener la **dirección de Ethereum**, se aplica la función hash **Keccak-256** a la clave pública comprimida y se toman los últimos **40 caracteres** hexadecimales (20 bytes). Por convención se añade el prefijo '0x' al inicio para indicar que es un valor hexadecimal. La dirección de Ethereum tiene por lo tanto **42 caracteres** (incluyendo '0x').

Para generar tus propias claves en Ethereum de manera práctica y educativa puedes utilizar herramientas como [**vanity-eth.tk**](https://vanity-eth.tk/). Esta página permite generar claves privadas y direcciones de Ethereum directamente en tu navegador, sin necesidad de descargar software adicional. Nuevamente recuerda que esta práctica debe ser solo con fines educativos y no para gestionar fondos reales.

```
// Clave privada (64 caracteres):
1c39abf0e8e0f8eab0a0f5c7d9e1d3b2f4a5c6d7e8f9a0b1c2d3e4f5a6b7c8d9

// Clave pública (128 caracteres):
04a34b5c6d7e8f9a0b1c2d3e4f5a6b7c8d9e0f1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b1c2d3e4f5a6b7c8d9e0f1a2b3c4d5e6f7a8b9c0d1e2f3a4b5

// Dirección de Ethereum (42 caracteres):
0xA9962326BFaf46775B345f85aA9a649867EA5D56
```

### Frase semilla

Además de la clave privada, también es común que se genere una **frase semilla**. Esta es una secuencia de palabras que actúa como respaldo de tu clave privada. La frase semilla suele estar compuesta por **12 o 24 palabras** elegidas de una lista estandarizada.

```
// Frase semilla (12 palabras):
poeta ave río cielo luna campo monte luz sombra tiempo flor viento
```

La frase semilla proviene de un número aleatorio con un alto nivel de entropía, y luego, este número se convierte en una serie de palabras seleccionadas de la lista estandarizada. Es crucial mantener esta frase en un lugar seguro, ya que cualquiera que tenga acceso a ella podrá controlar tu clave privada.

### Genera tu dirección de Ethereum de manera segura

Te guiaré paso a paso para que puedas generar tu par de claves, frase semilla y dirección de Ethereum en pocos pasos. Todo mediante una librería creada por mi exclusivamente para este curso.

1. Descarga e instala [Node.js](https://nodejs.org/en/).
2. Abre la terminal de comandos.
3. Ejecuta el siguiente comando para instalar la librería:

```
npm install -g eth-key-generator
```

4. Una vez instalado, puedes ejecutar la herramienta desde la línea de comandos:

```
eth-key-generator
```

5. Puedes seleccionar entre generar la dirección al azar o proporcionando entropía para dar mayor seguridad (solo debes ingresar una cadena de texto con cualquier palabra o frase).&#x20;
6. La herramienta generará una dirección de Ethereum nueva, mostrando cada paso del proceso.

Puedes usar esta librería las veces que desees, compartirla con más personas e incluso puedes proponer mejoras, acá te dejo el link al repositorio.

{% embed url="https://github.com/DavidZapataOh/ETH-KEY-GENERATOR" %}

{% hint style="info" %}
Esta herramienta es para fines educativos. No utilices las direcciones generadas para manejar fondos reales sin las precauciones adecuadas.
{% endhint %}

### Aquí empieza tu camino

Una vez que tienes tus claves, puedes interactuar con la blockchain de varias formas:

* **Enviar y recibir criptomonedas**: Utilizas tu clave privada para firmar transacciones que transfieren fondos desde tu dirección a otra. Esta firma garantiza que la transacción fue autorizada por el propietario legítimo.
* **Interactuar con contratos inteligentes**: Puedes enviar transacciones que ejecutan funciones en contratos inteligentes. Esto te permite interactuar en aplicaciones descentralizadas (dApps) y servicios DeFi.
* **Firmar mensajes**: Puedes demostrar que eres el propietario de una dirección firmando mensajes con tu clave privada, sin revelar la clave en sí. Esto es útil para autenticaciones y verificaciones en diferentes plataformas.
