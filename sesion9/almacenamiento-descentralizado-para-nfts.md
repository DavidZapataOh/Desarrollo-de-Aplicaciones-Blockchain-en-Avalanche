---
icon: square-small
---

# Almacenamiento Descentralizado para NFTs

En el mundo de los NFTs, cada token suele tener información única, como imágenes, nombres o descripciones, que forman sus **metadatos**. Sin embargo, esta información no se guarda directamente en la blockchain, ya que almacenar grandes cantidades de datos en la cadena puede ser caro y poco práctico. En su lugar, se usa **almacenamiento descentralizado** y una **URI** (Uniform Resource Identifier) para manejar estos datos de manera eficiente.

<figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

### **¿Qué es IPFS?**

**IPFS** (InterPlanetary File System) es un sistema de almacenamiento descentralizado que permite guardar y compartir archivos de forma segura y sin depender de un servidor central. En lugar de almacenar archivos en una ubicación específica (como un servidor), IPFS guarda los datos en una red de nodos (computadoras) distribuidos. Esto significa que:

* Los archivos subidos a IPFS obtienen un **CID** (Content Identifier), que es un identificador único basado en el contenido del archivo.
* Este **CID** sirve como una dirección permanente para el archivo, incluso si una copia del archivo se pierde en un nodo, IPFS encontrará otra copia en la red.
* IPFS garantiza que los datos sean inmutables: si el archivo cambia, también cambia su CID.

En el caso de los NFTs, se usa IPFS para almacenar las imágenes y metadatos de los tokens. Así, cada NFT puede apuntar a un archivo específico en IPFS que contiene su información única.

### **¿Qué es Base URI?**

El **Base URI** es una dirección base que se utiliza en el contrato ERC721 para construir el enlace a los metadatos de cada NFT. En lugar de guardar un enlace completo para cada token, se define un **Base URI** general y luego cada token utiliza su `tokenId` para acceder a sus datos específicos.

Por ejemplo, si configuramos el Base URI como:

```arduino
ipfs://QmXyZ.../collection/
```

Para el token con `tokenId` 1, el enlace completo a sus metadatos será:

```arduino
ipfs://QmXyZ.../collection/1
```

Este enfoque permite gestionar de forma eficiente los enlaces a los metadatos, haciendo que todos los NFTs de una colección compartan el mismo URI base pero tengan direcciones únicas según su `tokenId`.
