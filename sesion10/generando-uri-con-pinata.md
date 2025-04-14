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

# Generando URI con Pinata

**Pinata** es una plataforma que facilita el almacenamiento de archivos en **IPFS** (InterPlanetary File System). Vamos a usar Pinata para alojar las imágenes y los metadatos de tus NFTs en IPFS, obteniendo así una **Base URI** que podrás usar en tu contrato ERC721.



**1. Crear una Cuenta en Pinata**

* Visita [Pinata](https://www.pinata.cloud/) y regístrate para obtener una cuenta gratuita. Esta cuenta te permitirá subir y gestionar archivos en IPFS.

{% embed url="https://www.pinata.cloud/" %}

**2. Subir las Imágenes de tus NFTs a Pinata**

* En tu cuenta de Pinata, selecciona **"Add"** y elige **"File Upload"** para subir cada imagen individualmente o en lote.

<figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

* Cuando subes una imagen, Pinata generará un **CID** (Content Identifier), que es un identificador único que representa esa imagen en IPFS.
* **Nota**: Guarda el CID de cada imagen, ya que lo necesitarás para incluirlo en el campo `image` de los metadatos de cada NFT.

<figure><img src="../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

**3. Crear Archivos de Metadatos JSON**

Cada NFT necesita un archivo de metadatos JSON que contenga su información única, como el nombre, la descripción y el enlace de la imagen. A continuación tienes un ejemplo de cómo se vería un archivo JSON de metadatos para un NFT:

```json
{
  "name": "NFT #1",
  "description": "Este es el NFT número 1 de mi colección",
  "image": "ipfs://[CID_de_la_imagen]",
  "attributes": [
    {
      "trait_type": "Color",
      "value": "Rojo"
    },
    {
      "trait_type": "Tipo",
      "value": "Mago"
    }
  ]
}
```

* **Campo `image`**: Reemplaza `[CID_de_la_imagen]` con el CID de la imagen correspondiente en IPFS. Por ejemplo, si el CID de la imagen es `QmXyz123`, el campo `image` debería ser `"ipfs://QmXyz123"`.
* **Atributos**: Puedes incluir cualquier atributo que desees, como características específicas o niveles de rareza. Puedes dejarlo vacío o agregar más.

**4. Crear una Carpeta de Metadatos y Subirla a Pinata**

Para facilitar el acceso a todos los metadatos desde una misma URI base, organiza todos los archivos JSON en una **carpeta**. Luego:

* Sube la carpeta completa con los archivos JSON de metadatos a Pinata seleccionando **"Add"** > **"Folder Upload"**.
* Una vez que subas la carpeta, Pinata generará un **CID** único para la carpeta.

5.  **Obtener el Base URI**

    El CID de la carpeta se convierte en tu **Base URI** para la colección NFT. El formato de esta URI base será algo como:

    ```arduino
    ipfs://[CID_de_la_carpeta]/
    ```

    Cuando configures este **Base URI** en tu contrato ERC721, podrás acceder a los metadatos específicos de cada NFT añadiendo el `tokenId` correspondiente al final. Por ejemplo:

    * `ipfs://[CID_de_la_carpeta]/1` será el enlace para el NFT con `tokenId` 1.
    * `ipfs://[CID_de_la_carpeta]/2` para el NFT con `tokenId` 2, y así sucesivamente.

### Tu turno

Sube 3 imagenes cualquieras a Pinata y luego sube una carpeta con sus Metadatos. Usaremos el CID de la carpeta para los NFTs que creemos.
