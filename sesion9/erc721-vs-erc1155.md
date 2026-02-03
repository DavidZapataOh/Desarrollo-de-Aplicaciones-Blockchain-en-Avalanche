---
icon: square-small
---

# ERC721 vs ERC1155

Los estándares **ERC721** y **ERC1155** son protocolos en Ethereum para crear y gestionar NFTs, pero cada uno ofrece características específicas para diferentes tipos de activos y necesidades. La diferencia principal entre ellos está en cómo manejan la propiedad y la transferibilidad de los tokens no fungibles.

### ERC721

Fue el primer estándar ampliamente adoptado para NFTs. Cada token ERC721 es único e indivisible, lo cual lo convierte en una opción ideal para activos digitales como obras de arte o coleccionables, donde cada unidad debe mantenerse individual e irrepetible. Cada ERC721 tiene un identificador único (token ID) que lo distingue de cualquier otro token dentro del mismo contrato.

* **Ejemplo de uso:** Los **CryptoKitties**, una de las primeras aplicaciones populares de NFTs, utilizan el estándar ERC721, donde cada gato digital tiene características únicas y es completamente distinto de los demás.
* **Limitaciones:** Debido a su diseño, el ERC721 requiere una transacción para cada token individual que se quiera transferir, lo que puede resultar costoso y lento si se manejan muchos NFTs a la vez.

### ERC1155

**ERC1155** es una evolución del estándar ERC721 que permite gestionar tanto tokens fungibles como no fungibles en un solo contrato. A diferencia del ERC721, el ERC1155 permite transferir varios tokens en una única transacción, lo cual resulta en una mayor eficiencia y menores costos. Además, permite que un mismo contrato contenga varios tipos de activos, ideal para videojuegos o aplicaciones con múltiples elementos.

* **Ejemplo de uso:** En **Gods Unchained**, un juego de cartas digital, se utiliza ERC1155 para permitir a los jugadores poseer múltiples cartas en una sola transacción, ahorrando en costos de gas y tiempo.
* **Ventaja clave:** ERC1155 puede manejar tanto activos únicos (no fungibles) como activos intercambiables (fungibles), permitiendo, por ejemplo, que en un juego existan armas únicas (NFTs) y monedas intercambiables (tokens fungibles) bajo el mismo contrato.



| Característica   | ERC721                                  | ERC1155                                     |
| ---------------- | --------------------------------------- | ------------------------------------------- |
| **Unicidad**     | Solo NFTs únicos                        | NFTs y tokens fungibles                     |
| **Eficiencia**   | Una transacción por token               | Varias transferencias en una transacción    |
| **Aplicaciones** | Arte digital, coleccionables exclusivos | Videojuegos, sistemas con múltiples activos |
| **Costo de Gas** | Más alto en grandes cantidades          | Más bajo, ideal para múltiples tokens       |

Ambos estándares tienen fortalezas particulares. **ERC721** es perfecto para aquellos casos donde cada token debe ser único y completamente individual. **ERC1155**, en cambio, es ideal para aplicaciones que requieren manejar varios tipos de activos en un solo contrato y con menor consumo de gas, como en los videojuegos o en plataformas de comercio de múltiples ítems.

Ambos estándares son componentes clave en el ecosistema de los NFTs, y cada uno se adapta mejor según la necesidad de unicidad o eficiencia en la administración de activos.
