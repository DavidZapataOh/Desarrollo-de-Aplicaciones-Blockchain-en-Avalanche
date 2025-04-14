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

# Anatomía de un Bloque

Ahora que ya sabemos cómo se realiza una transacción y cómo seguirla en la blockchain, es momento de entender **qué es un bloque** y qué información contiene. Después de todo, la blockchain se llama así porque está formada por una cadena de bloques. Pero, ¿qué hay dentro de esos bloques?



Un bloque contiene varias partes importantes:

1. **Encabezado del Bloque:**
   * **Hash del Bloque Anterior:** Es como un sello que conecta cada bloque con el anterior, formando una cadena inquebrantable. Esto asegura que no se puedan alterar los bloques anteriores sin cambiar todos los que vienen después. Sin embargo, en el caso del **Bloque Génesis**, que es el primer bloque de la cadena, este campo está lleno de ceros, ya que no existe un bloque anterior. Esto indica que es el punto de inicio de la blockchain.
   * **Marca de Tiempo (Timestamp):** Indica la fecha y hora en que se creó el bloque. Así sabemos cuándo ocurrió cada cosa.
   * **Nonce:** Es un número que los mineros tienen que encontrar para poder agregar el bloque a la cadena. En **Proof of Work** los mineros compiten por descubrir este número resolviendo problemas matemáticos.
   * **Raíz de Merkle (Merkle Root):** Es como un resumen de todas las transacciones en el bloque. Permite verificar rápidamente si una transacción está incluida sin tener que revisar una por una.
2. **Cuerpo del Bloque:**
   * **Transacciones:** Aquí es donde se registran todas las transacciones que se incluyen en el bloque. Cada una tiene detalles como quién envía, quién recibe y cuánto se transfiere.

<figure><img src="../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

Prácticamente un bloque vendría siendo como una caja que contiene muchas transacciones y tiene etiquetas importantes que lo conectan con el bloque anterior y resumen su contenido.

Al estar todos los bloques conectados, si alguien intentara cambiar una transacción en un bloque anterior tendría que modificar todos los bloques siguientes, lo cual es prácticamente imposible en una red grande.

### Bloque Génesis

Hablando de bloques, no podemos olvidar el famoso **Bloque Génesis**. Este es el primer bloque de una blockchain, el punto de partida de todo. En el caso de Bitcoin, el Bloque Génesis fue creado por Satoshi Nakamoto el 3 de enero de 2009. Este bloque es especial porque no hace referencia a ningún bloque anterior (porque simplemente no existía). Además Satoshi incluyó en él un mensaje oculto: _"The Times 03/Jan/2009 Chancellor on brink of second bailout for banks"_, que era el titular de un periódico británico de ese día. Muchos ven esto como una crítica al sistema financiero tradicional y una declaración de intenciones sobre por qué nació Bitcoin.

El Bloque Génesis es fundamental porque establece las reglas iniciales y la estructura de la blockchain. Sin él no habría cadena que seguir. Cada bloque que se añade después se basa en el anterior, creando esa cadena de bloques que conocemos.



Ahora cuando escuches hablar de mineros resolviendo problemas matemáticos o de bloques siendo añadidos a la cadena, sabrás exactamente qué significa y por qué es tan importante. La blockchain es más que una simple lista de transacciones, es un sistema cuidadosamente diseñado para ser seguro, transparente y resistente a manipulaciones.
