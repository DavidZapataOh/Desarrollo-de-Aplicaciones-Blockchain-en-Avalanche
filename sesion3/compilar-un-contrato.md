---
icon: square-small
---

# Compilar un Contrato

Ya tenemos nuestro contrato, ahora lo que debemos hacer es compilarlo, este proceso convierte el código de alto nivel que escribiste en Solidity en un lenguaje que la blockchain pueda entender y ejecutar.

Cuando escribes un contrato inteligente en **Solidity**, lo haces en un lenguaje que es amigable para los desarrolladores, pero las blockchains no entienden directamente este código. Aquí es donde entra la **compilación**, convierte el código de Solidity en **bytecode**, que es el formato que la máquina virtual de Ethereum (EVM) puede ejecutar.

La compilación también genera algo llamado **ABI** (Application Binary Interface), que es un formato que describe cómo interactuar con el contrato, qué funciones tiene, qué entradas necesita y qué tipo de datos devuelve. Sin la ABI, las aplicaciones descentralizadas no sabrían cómo comunicarse con tu contrato.

Para compilar nuestro contrato, lo primero que haremos es dirigirnos a la sección "Solidity compiler" en el panel izquierdo:

<figure><img src="../.gitbook/assets/image (20) (1).png" alt=""><figcaption></figcaption></figure>



Asegurarte de que la versión el compilador entré dentro del rango que definiste en el pragma, en nuestro caso debería ser desde la 0.8.20 en adelante:

<figure><img src="../.gitbook/assets/image (21) (1).png" alt=""><figcaption></figcaption></figure>

Luego verás que hay 3 checkbox, te explicaré que hace cada una:

* **Include nightly builds:** Te permite usar las versiones más recientes y no estables del compilador de Solidity, conocidas como "nightly builds". Pueden ser inestables y contener errores no identificados todavía, por lo que se recomienda usarlas solo si necesitas probar algo específico que aún no ha sido lanzado oficialmente.
* **Auto compile:** Remix compilará automáticamente tu contrato cada vez que hagas un cambio en el código. Esta opción es útil porque te ahorra el esfuerzo de compilar manualmente cada vez que hagas un cambio, lo que te permite ver en tiempo real si hay errores o advertencias en el código a medida que lo escribes.
* **Hide warnings:** Te permite ocultar las advertencias generadas durante la compilación. Aunque las advertencias no son errores críticos, pueden indicar posibles problemas o malas prácticas en el código. Si decides ocultarlas, no verás estos mensajes en la consola, lo que podría hacer que te pierdas advertencias importantes que podrían prevenir errores futuros.

Para compilar tu contrato manualmente solo debes dar clic en el gran botón azul que dice **Compile** más el nombre del contrato. O también puedes hacerlo apretando **Ctrl + S.**

<figure><img src="../.gitbook/assets/image (23) (1).png" alt=""><figcaption></figcaption></figure>

Si no hay errores, se marcará un chulito verde en el icono del panel izquierdo, con el mensaje "Compilation successful".

Abajo verás otro botón en gris que dice "Compile and Run script", por lo general casi no se suele usar, su función es compilar e inmediatamente ejecutar scripts (generalmente de Javascript o Typescript) en el entorno de Remix. Yo recomendaría usar herramientas como Hardhat o Foundry en lugar de esto.

Un apartado que suele confundir a muchos es el que esta debajo, "CONTRACT". Un archivo `.sol` puede tener varios contratos, y a su vez, esos contratos pueden estar importando otros contratos. En este apartado puedes especificar cual de todos los contratos es el que quieres compilar. En nuestro caso solo tenemos un contrato, por lo que de momento no tenemos de qué preocuparnos.

<figure><img src="../.gitbook/assets/image (24) (1).png" alt=""><figcaption></figcaption></figure>

Eso sería suficiente para poder compilar nuestros contratos con tranquilidad, pero hay veces que por distintas circunstancias, deberemos usar las configuraciones avanzadas.

<figure><img src="../.gitbook/assets/image (25) (1).png" alt=""><figcaption></figcaption></figure>

* Primero te da a elegir si quieres elegir configurar el compilador a través de la interfaz o mediante un archivo .JSON, por defecto será mediante la interfaz.
* Luego te pedirá definir el lenguaje que usarás para escribir los contratos inteligente, te dará dos opciones, Solidity o YUL (una representación intermedia utilizada por Solidity), pero en la mayoría de los casos, **Solidity** es lo que necesitas.
* La lista desplegable EVM te permite compilar código con una **versión de Ethereum** específica. Generalmente se suele dejar por defecto.
* **Enable optimization** te permite habilitar la **optimización** durante la compilación. Cuando está activada, el compilador intenta reducir el tamaño del bytecode del contrato o el uso de gas (coste de las transacciones). Puedes ajustar el número de iteraciones para determinar cuánto deseas optimizar el contrato, aunque el valor predeterminado (200) suele ser suficiente en la mayoría de los casos.



Remix también nos ofrece una serie de herramientas que podemos usar al compilar nuestro contrato:

<figure><img src="../.gitbook/assets/image (26) (1).png" alt=""><figcaption></figcaption></figure>

* **Run Remix Analysis:** Analiza tu contrato buscando errores y advertencias de seguridad y optimización. Sin embargo, es una herramienta relativamente nueva, por lo cual, aún tiene demasiados fallos y tiende a confundirse.&#x20;
* **Run SolidityScan:** Realiza un análisis de seguridad para detectar vulnerabilidades específicas en el contrato.
* **Publish on IPFS:** Publica tu contrato en una red descentralizada para compartir archivos (IPFS), haciendo el código accesible públicamente.
* **Publish on Swarm:** Es similar a IPFS, te permite almacenar tu contrato en una red descentralizada específica del ecosistema Ethereum.
* **Compilation Details:** Proporciona detalles técnicos como el bytecode, la ABI y el uso estimado de gas, y otras informaciones importantes que se generan durante la compilación.



Por ultimo, abajo de todo tenemos la opción de copiar el **ABI** y el **Bytecode**.

<figure><img src="../.gitbook/assets/image (28) (1).png" alt=""><figcaption></figcaption></figure>
