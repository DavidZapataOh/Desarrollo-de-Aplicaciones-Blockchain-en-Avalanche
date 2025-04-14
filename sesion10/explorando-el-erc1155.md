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

# Explorando el ERC1155

El **ERC1155** es un estándar de Ethereum que define un conjunto de funciones y eventos para crear y manejar múltiples tipos de tokens en un solo contrato. A diferencia de los estándares ERC20 y ERC721, **ERC1155** permite tanto tokens fungibles (intercambiables) como no fungibles (únicos) bajo el mismo contrato, lo cual optimiza los costos de gas y simplifica el almacenamiento y la transferencia de estos tokens.



### Componentes Clave del ERC721

El estándar **ERC721** define varias funciones y eventos esenciales que todos los contratos de tokens deben implementar:

**1. Funciones principales:**

1. **`constructor`:** Inicializa el contrato estableciendo un URI base para todos los tipos de token. El URI base utiliza un mecanismo de sustitución por el `id` del token, lo que permite que cada token apunte a su metadato correspondiente.
   * **Parámetros:** `uri_` (URI base de los tokens, donde `{id}` se sustituirá por el ID específico del token).
   * **Ejemplo**: [`ipfs://QmZTsFjJGALEVPHcMYGdS1F3xgpAnELUC8KwjijXqXrdNM/1.json`](https://ipfs.io/ipfs/QmZTsFjJGALEVPHcMYGdS1F3xgpAnELUC8KwjijXqXrdNM/1.json)
2. **`uri(uint256 id)`**: Devuelve la URI para un tipo específico de token. La URI usa `{id}` como marcador que será reemplazado por el identificador del token en las aplicaciones compatibles.
   * **Parámetro**: `id` (identificador único del tipo de token).
   * **Retorna**: La URI del token como una cadena de texto (string).
3. **`balanceOf(address account, uint256 id)`**: Devuelve el balance de tokens de un tipo específico para una dirección dada.
   * **Parámetro:** `account` (la dirección a consultar).
   * **Retorna:** El número de tokens que posee esa dirección (uint256).
4. **`balanceOfBatch(address[] memory accounts, uint256[] memory ids)`**: Devuelve el balance de varios tipos de tokens para múltiples direcciones en una sola llamada.
   * **Parámetros**: `accounts` (direcciones a consultar) y `ids` (identificadores de los tipos de tokens).
   * **Retorna**: Un arreglo con los balances correspondientes a cada dirección y tipo de token.
5. **`setApprovalForAll(address operator, bool approved)`**: Permite o revoca la autorización de otra dirección para manejar todos los tokens del propietario.
   * **Parámetros**: `operator` (dirección que se desea autorizar) y `approved` (si se autoriza o revoca).
   * **Retorna**: `true` si la operación es exitosa.
6. **`isApprovedForAll(address owner, address operator)`**: Verifica si una dirección está autorizada para manejar todos los tokens de un propietario.
   * **Parámetros**: `owner` (propietario de los tokens) y `operator` (dirección a verificar).
   * **Retorna**: `true` si la dirección tiene permisos para manejar todos los tokens.
7. **`safeTransferFrom(address from, address to, uint256 id, uint256 value, bytes memory data)`**: Transfiere una cantidad específica de tokens de un tipo desde una dirección a otra.
   * **Parámetros**: `from`, `to`, `id`, `value`, y `data` (datos adicionales, opcional).
   * **Requisitos**: `from` debe tener suficiente balance de tokens y `to` no debe ser la dirección cero.
8. **`safeBatchTransferFrom(address from, address to, uint256[] memory ids, uint256[] memory values, bytes memory data)`**: Transfiere múltiples tipos de tokens en una sola operación.
   * **Parámetros**: `from`, `to`, `ids`, `values`, y `data`.
   * **Requisitos**: `from` debe tener suficiente balance de tokens de cada tipo en `ids`.
9. **\_setURI(string memory newuri)**: Función interna que establece un nuevo URI para todos los tipos de tokens, aplicando el mecanismo de sustitución por `id`.
   * **Parámetro**: `newuri` (nuevo URI base).
10. **`_mint(address to, uint256 id, uint256 value, bytes memory data)`**: Crea una cantidad específica de tokens de un tipo determinado y los asigna a una dirección.
    * **Parámetros**: `to`, `id`, `value`, y `data`.
    * **Requisitos**: `to` no debe ser la dirección cero
11. **`_mintBatch(address to, uint256[] memory ids, uint256[] memory values, bytes memory data)`**: Crea múltiples tipos de tokens en una sola llamada y los asigna a una dirección.
    * **Parámetros**: `to`, `ids`, `values`, y `data`.
12. **`_burn(address from, uint256 id, uint256 value)`**: Destruye una cantidad específica de tokens de un tipo para una dirección determinada.
    * **Parámetros**: `from`, `id`, `value`.
13. **`_burnBatch(address from, uint256[] memory ids, uint256[] memory values)`**: Destruye múltiples tipos de tokens en una sola llamada.
    * **Parámetros**: `from`, `ids`, y `values`.

**2. Eventos principales:**

1. **`TransferSingle(address indexed operator, address indexed from, address indexed to, uint256 id, uint256 value)`**: Se emite cada vez que un token de un solo tipo es transferido de una dirección a otra.
2. **`TransferBatch(address indexed operator, address indexed from, address indexed to, uint256[] ids, uint256[] values)`**: Se emite cuando múltiples tipos de tokens son transferidos en una sola operación.
3. **`ApprovalForAll(address indexed account, address indexed operator, bool approved)`**: Se emite cuando una dirección permite o revoca el manejo de sus tokens a un operador.



### ¿Por qué es tan importante el ERC1155?

* **Eficiencia en Costos de Gas**: Al agrupar múltiples tipos de tokens en un solo contrato, **ERC1155** reduce los costos de gas, especialmente cuando se realizan transferencias en lote.
* **Flexibilidad**: Soporta tanto tokens fungibles como no fungibles en el mismo contrato, lo que lo hace ideal para aplicaciones como videojuegos, donde los jugadores pueden tener múltiples activos (monedas, ítems únicos, etc.).
* **Gestión Simplificada**: Al utilizar una estructura común para varios tipos de tokens, **ERC1155** permite una administración más sencilla y eficiente de grandes cantidades de activos digitales.

### Ejemplo de Contrato ERC1155

Aquí tienes un ejemplo básico de un contrato ERC1155 utilizando OpenZeppelin:

```solidity
// SPDX-License-Identifier: MIT
import "@openzeppelin/contracts/token/ERC1155/ERC1155.sol";

contract MiTokenMulti is ERC1155 {
    constructor() ERC1155("ipfs://QmZTsFjJGALEVPHcMYGdS1F3xgpAnELUC8KwjijXqXrdNM/1.json") {}

    function mint(address account, uint256 id, uint256 amount, bytes memory data) public {
        _mint(account, id, amount, data);
    }

    function mintBatch(address to, uint256[] memory ids, uint256[] memory amounts, bytes memory data) public {
        _mintBatch(to, ids, amounts, data);
    }
}
```

* **Importación**: Se importa el contrato ERC1155 de OpenZeppelin, lo que asegura que se sigan todas las reglas del estándar.
* **URI Base**: Al implementar `ERC1155`, se establece un URI que incluye `{id}`, el cual se reemplazará con el `id` del token correspondiente en cada solicitud de URI.
