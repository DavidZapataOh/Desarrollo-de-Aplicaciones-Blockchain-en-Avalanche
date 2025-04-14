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

# Explorando el ERC721

El **ERC721** es un estándar que define un conjunto de funciones y eventos para crear y manejar NFTs (tokens no fungibles). Este estándar permite que cada token tenga un identificador único, lo que lo diferencia de otros tokens y asegura su individualidad. Piensa en el ERC721 como un conjunto de reglas que permiten a los NFTs funcionar de manera uniforme en aplicaciones, wallets y marketplaces, asegurando que todos los tokens no fungibles hablen el mismo "idioma".



### Componentes Clave del ERC721

El estándar **ERC721** define varias funciones y eventos esenciales que todos los contratos de tokens deben implementar:

**1. Funciones principales:**

1. **`constructor`:** Establece el nombre y el símbolo del token cuando se despliega el contrato. Estos valores son inmutables y no pueden cambiarse después de la creación.
   * **Parámetros:** `name_` (nombre del token) y `symbol_` (símbolo del token).
   * **Ejemplo**: Si creas un token con `constructor("MiTokenUnico", "MTU")`, el nombre será "MiTokenUnico" y el símbolo "MTU".
2. **`name()`:** Devuelve el nombre del token. Es una función de solo lectura y su valor se establece durante la construcción del contrato.
   * **Retorna:** El nombre del token como una cadena de texto (`string`).
3. **`symbol()`:** Devuelve el símbolo del token, generalmente una abreviatura o versión corta del nombre.
   * **Retorna:** El símbolo del token (`string`).
4. **`tokenURI(uint256 tokenId)`**: Proporciona un enlace (URI) a los metadatos del token, que suelen incluir información como el nombre, la descripción e imágenes.
   * **Parámetro**: `tokenId` (identificador único del token).
   * **Retorna**: El URI (string) que apunta a los metadatos del token.
5. **\_baseURI()**: Función interna que establece la URI base para todos los tokens.
   * **Retorna**: El URI base (string) para los tokens, puede ser sobrescrito en contratos heredados.
6. **`balanceOf(address account)`:** Devuelve la cantidad de tokens en posesión de una dirección específica.
   * **Parámetro:** `account` (la dirección a consultar).
   * **Retorna:** El número de tokens que posee esa dirección (uint256).
7. **`ownerOf(uint256 tokenId)`:** Devuelve la dirección que posee un token específico.
   * **Parámetro:** `tokenId` (identificador del token).
   * **Retorna:** La dirección del propietario (address).
8. **`safeTransferFrom(address from, address to, uint256 tokenId)`**: Transfiere un token de manera segura desde el propietario a otra dirección.
   * **Parámetros:** `from` (dirección del propietario actual), `to` (dirección del receptor) y `tokenId` (identificador del token a transferir).
   * **Requisitos:** El emisor debe poseer el token o tener la aprobación del propietario.
   * **Retorna:** `true` si la transferencia fue exitosa.
9. **`approve(address to, uint256 tokenId)`**: Autoriza a otra dirección a transferir un token en nombre del propietario.
   * **Parámetros**: `to` (dirección autorizada) y `tokenId` (identificador del token).
   * **Retorna**: `true` si la aprobación es exitosa.
10. **`setApprovalForAll(address operator, bool approved)`**: Permite o revoca la autorización de otra dirección para manejar todos los tokens del propietario.
    * **Parámetros**: `operator` (dirección que se desea autorizar) y `approved` (si se autoriza o revoca).
    * **Retorna**: `true` si la operación es exitosa.
11. **`getApproved(uint256 tokenId)`**: Devuelve la dirección autorizada para transferir un token específico.
    * **Parámetro**: `tokenId` (identificador del token).
    * **Retorna**: Dirección autorizada (address).
12. **`isApprovedForAll(address owner, address operator)`**: Verifica si una dirección está autorizada para manejar todos los tokens de un propietario.
    * **Parámetros**: `owner` (propietario de los tokens) y `operator` (dirección a verificar).
    * **Retorna**: `true` si la dirección tiene permisos para manejar todos los tokens.
13. **`_isAuthorized(address owner, address spender, uint256 tokenId)`**: Verifica si una dirección está autorizada para manejar un token específico.
    * **Parámetros**: `owner`, `spender`, `tokenId`.
    * **Retorna**: `true` si la dirección tiene autorización.
14. **`_checkAuthorized(address owner, address spender, uint256 tokenId)`**: Verifica y revierte si una dirección no está autorizada para manejar un token.
    * **Parámetros**: `owner`, `spender`, `tokenId`.
    * **Uso**: Evita acciones no autorizadas en el token.
15. **`_update(address to, uint256 tokenId, address auth)`**: Transfiere `tokenId` a `to` o realiza minting/burning si corresponde.
    * **Parámetros**: `to`, `tokenId`, `auth`.
    * **Retorna**: El propietario previo.
16. **`_safeMint(address to, uint256 tokenId)`**: Versión segura de `_mint` que verifica la aceptación del receptor.
    * **Parámetro:** `account` (dirección a la que se asignan los tokens) y `value` (cantidad de tokens creados).
17. **`_burn(address account, uint256 value)`**: Destruye tokens de la cuenta especificada, reduciendo la oferta total de tokens.
    * **Parámetros**: `to`, `tokenId`.
18. **`_safeMint(address to, uint256 tokenId)`**: Versión segura de `_mint` que verifica la aceptación del receptor.
    * **Parámetros**: `to`, `tokenId`.
19. **`_burn(uint256 tokenId)`**: Destruye un token y borra su propiedad.
    * **Parámetro**: `tokenId`.

**2. Eventos principales:**

1. **`Transfer(address indexed from, address indexed to, uint256 indexed tokenId)`**: Se emite cada vez que un token se transfiere de una dirección a otra.
2. **Approval(address indexed owner, address indexed approved, uint256 indexed tokenId)**: Se emite cuando el propietario de un token autoriza a otra dirección a transferir el token.
3. **ApprovalForAll(address indexed owner, address indexed operator, bool approved)**: Se emite cuando el propietario permite o revoca la autorización de un operador para manejar todos sus tokens.

### ¿Por qué es tan importante el ERC721?

* **Interoperabilidad**: Al estandarizar las funciones, los NFTs basados en ERC721 pueden ser transferidos y utilizados en cualquier wallet o plataforma que soporte este estándar.
* **Unicidad y Autenticidad**: Cada token ERC721 es único, lo que lo convierte en una excelente opción para representar activos digitales exclusivos o coleccionables.
* **Gestión de Permisos**: Con funciones como `approve` y `setApprovalForAll`, el ERC721 permite un control granular de la propiedad y la delegación de permisos para transferencias.

### Contrato ERC721

Aquí te muestro cómo se vería un contrato ERC721 básico utilizando OpenZeppelin, una biblioteca que simplifica la implementación de contratos seguros y estándar:

```solidity
// Importamos el contrato ERC721 de OpenZeppelin
import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

// Creamos un contrato ERC721 llamado "ColeccionNFT"
contract ColeccionNFT is ERC721 {
    constructor() ERC721("ColeccionNFT", "CNFT") {}

    function mintNFT(address recipient, uint256 tokenId) public {
        _safeMint(recipient, tokenId);
    }
}
```

* **Importación**: Se importa la implementación estándar de ERC721 de OpenZeppelin, asegurando que se sigan todas las reglas del estándar.
* **Creación del Token**: Se inicializa un token llamado "ColeccionNFT" con el símbolo "CNFT". Este contrato permite acuñar nuevos NFTs de manera segura y asignarlos a una dirección específica con `mintNFT`.
