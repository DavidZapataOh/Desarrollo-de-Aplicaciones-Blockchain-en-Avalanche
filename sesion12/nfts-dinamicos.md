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

# NFTs Dinámicos

Los **NFTs dinámicos** representan una evolución significativa en la tecnología de tokens no fungibles, ya que permiten que los metadatos del NFT cambien en respuesta a ciertos eventos o condiciones. En el contexto de **Real World Assets (RWA)**, los NFTs dinámicos presentan una oportunidad única para representar activos cuyo valor, propiedades o estado pueden variar con el tiempo, proporcionando una representación más precisa y en tiempo real de los activos del mundo real.

### **¿Qué es un NFT Dinámico?**

Un **NFT dinámico** es un token no fungible cuya información o metadatos pueden actualizarse automáticamente en función de cambios en el mundo real o en la blockchain. A diferencia de los NFTs tradicionales, que poseen características fijas, los NFTs dinámicos pueden adaptarse a condiciones específicas mediante la integración de **oráculos**, **contratos inteligentes** y **eventos externos**.

Ejemplo: Imagina que posees un NFT que representa un bien inmueble. Con un NFT dinámico, el valor de mercado de la propiedad, su estado o cualquier renovación que se le haga, puede reflejarse automáticamente en el NFT a medida que ocurren estos cambios.

### **Casos de Uso de NFTs Dinámicos en RWA**

1. **Propiedades Inmobiliarias**
   * Los NFTs dinámicos pueden representar propiedades cuyos valores de mercado fluctúan con el tiempo. Cada cambio en el valor, como una remodelación o una actualización en la tasación, puede reflejarse automáticamente en el NFT.
   * **Ejemplo práctico**: Un NFT que representa un edificio puede actualizar su valor cada trimestre según el precio del mercado local, mostrando también información sobre el estado de la propiedad, como si necesita reparaciones o si ha sido remodelada recientemente.
2. **Automóviles y Bienes Duraderos**
   * Para activos como automóviles, un NFT dinámico puede registrar el kilometraje, el historial de mantenimiento y el desgaste, permitiendo a los compradores potenciales evaluar el estado actual del vehículo sin depender de intermediarios.
   * **Ejemplo práctico**: Un NFT de un automóvil que cambia su valor y condiciones cada vez que se realiza una reparación importante o después de una revisión técnica, permitiendo a los compradores tener un historial actualizado en todo momento.
3. **Instrumentos Financieros y Valores**
   * Los NFTs dinámicos pueden representar bonos, acciones y otros instrumentos financieros cuyos valores y condiciones cambian en tiempo real.
   * **Ejemplo práctico**: Un bono tokenizado como NFT puede reflejar automáticamente los pagos de intereses realizados y los cambios en la tasa de interés, brindando a los inversionistas una vista actualizada de su inversión.
4. **Commodities y Recursos Naturales**
   * Activos como el oro, el petróleo y otros commodities pueden tokenizarse en NFTs dinámicos que reflejan el valor de mercado actual y las variaciones en su cantidad o calidad.
   * **Ejemplo práctico**: Un NFT que representa una mina de oro podría actualizar el valor de las reservas restantes y reflejar el precio actual del oro, brindando una representación en tiempo real de los recursos disponibles.

### **Implementación de un NFT Dinámico: Contrato RealEstateNFT**

A continuación, un contrato que representa un **NFT dinámico** para un activo del mundo real, como una propiedad inmobiliaria, cuyo valor se actualiza automáticamente según los datos proporcionados por un oráculo (simulado aquí). Este ejemplo utiliza **OpenZeppelin** para las funciones básicas de un NFT y **Chainlink** como oráculo de precios:

```solidity
solidityCopiar código// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@chainlink/contracts/src/v0.8/interfaces/AggregatorV3Interface.sol";

contract RealEstateNFT is ERC721URIStorage, Ownable {
    uint256 public tokenId;
    AggregatorV3Interface internal priceFeed;

    // Mapeo para almacenar los valores actuales de los activos
    mapping(uint256 => uint256) public assetValues;

    // Evento para el cambio de valor del NFT
    event AssetValueUpdated(uint256 tokenId, uint256 newValue);

    constructor(address _priceFeed) ERC721("RealEstateNFT", "REALE") {
        priceFeed = AggregatorV3Interface(_priceFeed);
    }

    // Función para mintear un nuevo NFT y establecer un valor inicial
    function mintNFT(address recipient, string memory tokenURI, uint256 initialValue) public onlyOwner {
        _mint(recipient, tokenId);
        _setTokenURI(tokenId, tokenURI);
        assetValues[tokenId] = initialValue;
        tokenId++;
    }

    // Función para actualizar el valor del activo desde un oráculo externo
    function updateAssetValue(uint256 _tokenId) public onlyOwner {
        require(_exists(_tokenId), "Token no existe.");
        
        // Obtener el precio actual desde el oráculo (simulado)
        (, int price, , ,) = priceFeed.latestRoundData();
        uint256 newValue = uint256(price);

        // Actualizar el valor del activo
        assetValues[_tokenId] = newValue;
        
        emit AssetValueUpdated(_tokenId, newValue);
    }

    // Obtener el valor actual del activo
    function getAssetValue(uint256 _tokenId) public view returns (uint256) {
        require(_exists(_tokenId), "Token no existe.");
        return assetValues[_tokenId];
    }
}
```

1. **Imports**: Este contrato utiliza la extensión `ERC721URIStorage` de OpenZeppelin para manejar los URIs de los tokens y `Ownable` para controlar las funciones solo para el propietario.
2. **Oráculo de Precios**: Este contrato asume la existencia de un oráculo (por ejemplo, Chainlink) que proporciona el valor del activo. Aquí, se inicializa el oráculo en el constructor.
3. **Minting del NFT**: La función `mintNFT` permite al propietario crear un nuevo NFT para representar un activo inmobiliario. A cada token se le asigna un URI y un valor inicial.
4. **Actualización de Valor**: La función `updateAssetValue` obtiene el valor más reciente del activo desde el oráculo y actualiza el valor del token en el contrato. Esta actualización solo puede ser realizada por el propietario del contrato.
5. **Consulta de Valor**: La función `getAssetValue` permite a cualquier usuario verificar el valor actual del activo representado por el NFT.

### **Beneficios de los NFTs Dinámicos en RWA**

Los NFTs dinámicos brindan **transparencia y precisión** en la representación de activos del mundo real. Con este enfoque, los inversionistas pueden acceder a una vista en tiempo real de su activo sin necesidad de intermediarios, lo cual permite mejorar la confianza y eficiencia en el mercado de activos tokenizados.
