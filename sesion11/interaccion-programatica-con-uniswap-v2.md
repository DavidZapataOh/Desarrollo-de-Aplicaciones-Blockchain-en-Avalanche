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

# Interacción Programática con Uniswap V2

La **interacción programática con Uniswap V2** permite a los desarrolladores integrar y automatizar operaciones como swaps de tokens, agregación de liquidez y consulta de precios directamente desde contratos inteligentes o aplicaciones descentralizadas (dApps). Esto es posible gracias a los contratos y las interfaces que Uniswap ofrece para interactuar con sus pools de liquidez y realizar transacciones descentralizadas.

### **Realizando un Swap de Tokens**

Para realizar un **swap de tokens** en Uniswap V2, se utiliza el contrato **UniswapV2Router02**. Este contrato contiene varias funciones para intercambiar tokens, como `swapExactTokensForTokens`, `swapTokensForExactTokens`, entre otros. A continuación, se detalla un ejemplo básico de cómo ejecutar un swap en Uniswap.

1.  **Configurar el Contrato Router**: La dirección del contrato `UniswapV2Router02` debe estar disponible en el script.&#x20;

    Para la red principal de Ethereum, la dirección es: `0x7a250d5630B4cF539739dF2C5dAcb4c659F2488D`.

    Para la red de Sepolia, la dirección es:

    `0xeE567Fe1712Faf6149d80dA1E6934E354124CfE3`.
2. **Realizar un Swap Exacto de Tokens**:
   * La función `swapExactTokensForTokens` permite intercambiar una cantidad específica de un token por otro, respetando un mínimo de salida especificado.
   *   Ejemplo en Solidity:

       ```solidity
       function swapTokens(address tokenIn, address tokenOut, uint amountIn, uint amountOutMin, address to) external {
           IERC20(tokenIn).approve(address(router), amountIn);
           address;
           path[0] = tokenIn;
           path[1] = tokenOut;

           router.swapExactTokensForTokens(
               amountIn,
               amountOutMin,
               path,
               to,
               block.timestamp
           );
       }
       ```
   * **Parámetros Clave**:
     * `amountIn`: Cantidad de tokens que el usuario quiere intercambiar.
     * `amountOutMin`: Cantidad mínima de tokens que el usuario acepta recibir, para protegerse de cambios en el precio.
     * `path`: Ruta de intercambio; en este caso, contiene dos direcciones de tokens (token de entrada y de salida).
     * `to`: Dirección que recibirá los tokens de salida.
     * `block.timestamp`: Define la validez temporal de la transacción para evitar demoras.

### **Intercambio Programático de AVAX y USDC en Uniswap**

Imaginemos que un usuario desea intercambiar **AVAX por USDC** utilizando Uniswap V2. El script de Solidity para realizar esta operación programáticamente es similar al ejemplo de `swapExactTokensForTokens`, configurado con AVAX como `tokenIn` y USDC como `tokenOut`. Esta transacción tomará la cantidad especificada de AVAX y calculará automáticamente el equivalente en USDC basado en la liquidez del pool.

### **Añadir y Retirar Liquidez**

Además del intercambio de tokens, Uniswap V2 permite agregar y retirar liquidez de los pools, lo que es esencial para los usuarios que desean ganar comisiones de transacción al proporcionar liquidez.

1. **Agregar Liquidez**: La función `addLiquidity` permite depositar una cantidad igual de dos tokens en un pool de Uniswap, a cambio de tokens LP (Liquidity Provider tokens) que representan su participación.
   *   Ejemplo en Solidity:

       ```solidity
       function addLiquidity(address tokenA, address tokenB, uint amountADesired, uint amountBDesired, address to) external {
           IERC20(tokenA).approve(address(router), amountADesired);
           IERC20(tokenB).approve(address(router), amountBDesired);

           router.addLiquidity(
               tokenA,
               tokenB,
               amountADesired,
               amountBDesired,
               0,
               0,
               to,
               block.timestamp
           );
       }
       ```
   * **Parámetros**:
     * `amountADesired` y `amountBDesired`: Cantidad de cada token que se desea depositar en el pool.
     * `0` en `amountAMin` y `amountBMin` asegura que no se acepten menos tokens de los deseados en caso de slippage.
     * `to`: Dirección que recibirá los tokens LP.
2. **Retirar Liquidez**: Para retirar tokens del pool y recuperar el monto proporcionado, se utiliza `removeLiquidity`.
   *   Ejemplo en Solidity:

       ```solidity
       function removeLiquidity(address tokenA, address tokenB, uint liquidity, address to) external {
           IERC20(pair).approve(address(router), liquidity);

           router.removeLiquidity(
               tokenA,
               tokenB,
               liquidity,
               0,
               0,
               to,
               block.timestamp
           );
       }
       ```
   * Aquí se pasa el monto de **tokens LP** y el contrato devuelve los tokens proporcionados, junto con las recompensas de comisiones acumuladas.

### Codigo completo

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/IERC20.sol";
import "@uniswap/v2-periphery/contracts/interfaces/IUniswapV2Router02.sol";
import "@uniswap/v2-core/contracts/interfaces/IUniswapV2Factory.sol";

contract UniswapInteraction {
    IUniswapV2Router02 public router;
    address public owner;

    // Constructor para inicializar el contrato y definir la dirección del router de Uniswap V2
    constructor(address _router) {
        router = IUniswapV2Router02(_router);
    }

    // Función para realizar un swap exacto de tokens en Uniswap
    function swapTokens(
        address tokenIn,
        address tokenOut,
        uint amountIn,
        uint amountOutMin,
        address to
    ) external {
        IERC20(tokenIn).approve(address(router), amountIn);

        address;
        path[0] = tokenIn;
        path[1] = tokenOut;

        router.swapExactTokensForTokens(
            amountIn,
            amountOutMin,
            path,
            to,
            block.timestamp
        );
    }

    // Función para agregar liquidez al pool de Uniswap
    function addLiquidity(
        address tokenA,
        address tokenB,
        uint amountADesired,
        uint amountBDesired,
        address to
    ) external {
        IERC20(tokenA).approve(address(router), amountADesired);
        IERC20(tokenB).approve(address(router), amountBDesired);

        router.addLiquidity(
            tokenA,
            tokenB,
            amountADesired,
            amountBDesired,
            0,
            0,
            to,
            block.timestamp
        );
    }

    // Función para retirar liquidez del pool de Uniswap
    function removeLiquidity(
        address tokenA,
        address tokenB,
        uint liquidity,
        address to
    ) external {
        address pair = IUniswapV2Factory(router.factory()).getPair(tokenA, tokenB);
        IERC20(pair).approve(address(router), liquidity);

        router.removeLiquidity(
            tokenA,
            tokenB,
            liquidity,
            0,
            0,
            to,
            block.timestamp
        );
    }
}

```
