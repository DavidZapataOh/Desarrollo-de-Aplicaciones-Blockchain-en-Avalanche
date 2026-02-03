---
icon: square-small
---

# Interacción Programática con Uniswap V3

La **interacción programática con Uniswap V3** permite a los desarrolladores realizar swaps, crear y gestionar pools de liquidez, y ajustar precios con precisión gracias a la nueva estructura de liquidez concentrada. A diferencia de Uniswap V2, V3 introduce características avanzadas como rangos de precios personalizables y múltiples niveles de tarifas, lo cual brinda a los proveedores de liquidez mayor control sobre sus inversiones.

### **Diferencias Clave entre Uniswap V2 y V3**

* **Liquidez Concentrada**: A diferencia de V2, los proveedores de liquidez pueden especificar rangos de precios en los que desean proporcionar liquidez en V3. Esto permite una mayor eficiencia de capital.
* **Niveles de Tarifas**: V3 permite elegir entre varios niveles de tarifas (0.01%, 0.05%, 0.3% y 1%) para adaptarse a la volatilidad y al riesgo de cada par de tokens.
* **NFTs para Liquidez**: En lugar de tokens LP, cada posición de liquidez en Uniswap V3 se representa mediante un NFT, que contiene información única sobre el rango de precios y el nivel de tarifa.

### **Realizando un Swap de Tokens**

En Uniswap V3, los swaps pueden realizarse usando el contrato `SwapRouter`. Aquí se muestra un ejemplo de cómo programar un swap de tokens de AVAX a USDC utilizando Uniswap V3:

1.  **Configuración del Contrato de Swap**:

    * Ejemplo de una función para realizar un swap exacto en Uniswap V3:

    ```solidity
    function swapExactInputSingle(address tokenIn, address tokenOut, uint24 fee, uint256 amountIn, address recipient) external returns (uint256 amountOut) {
        // Approbar el token de entrada para el router
        IERC20(tokenIn).approve(address(swapRouter), amountIn);
        
        // Configurar los parámetros para el swap
        ISwapRouter.ExactInputSingleParams memory params =
            ISwapRouter.ExactInputSingleParams({
                tokenIn: tokenIn,
                tokenOut: tokenOut,
                fee: fee,
                recipient: recipient,
                deadline: block.timestamp,
                amountIn: amountIn,
                amountOutMinimum: 0,
                sqrtPriceLimitX96: 0
            });

        // Ejecutar el swap
        amountOut = swapRouter.exactInputSingle(params);
    }
    ```

    * **Parámetros Importantes**:
      * `fee`: Nivel de tarifa para el par (por ejemplo, 3000 para 0.3%).
      * `amountIn` y `amountOutMinimum`: Cantidad de entrada y salida mínima para protegerse de cambios de precios.
      * `sqrtPriceLimitX96`: Límite de precio en formato raíz cuadrada, que en este caso se establece en cero para permitir cualquier precio.

### **Añadir y Retirar Liquidez**

En Uniswap V3, al agregar y retirar liquidez, se especifica un rango de precios. Esto permite a los proveedores de liquidez optimizar el uso de su capital y maximizar sus rendimientos.

1.  **Agregar Liquidez en un Rango de Precios**:

    * Ejemplo de función para añadir liquidez:

    ```solidity
    function addLiquidity(
        address tokenA,
        address tokenB,
        uint24 fee,
        int24 tickLower,
        int24 tickUpper,
        uint256 amountA,
        uint256 amountB,
        address recipient
    ) external returns (uint256 tokenId, uint128 liquidity, uint256 amount0, uint256 amount1) {
        // Configurar los parámetros para la adición de liquidez
        INonfungiblePositionManager.MintParams memory params =
            INonfungiblePositionManager.MintParams({
                token0: tokenA,
                token1: tokenB,
                fee: fee,
                tickLower: tickLower,
                tickUpper: tickUpper,
                amount0Desired: amountA,
                amount1Desired: amountB,
                amount0Min: 0,
                amount1Min: 0,
                recipient: recipient,
                deadline: block.timestamp
            });

        // Añadir liquidez y recibir un NFT de posición
        return nonfungiblePositionManager.mint(params);
    }
    ```

    * **Parámetros Clave**:
      * `tickLower` y `tickUpper`: Determinan el rango de precios donde se proveerá liquidez.
      * `amount0Min` y `amount1Min`: Cantidades mínimas que el usuario acepta proporcionar.
      * `recipient`: Dirección que recibe el NFT de posición.
2.  **Retirar Liquidez**:

    * Los proveedores de liquidez pueden retirar su liquidez devolviendo el NFT de su posición.

    ```solidity
    function removeLiquidity(
        uint256 tokenId,
        uint128 liquidity
    ) external returns (uint256 amount0, uint256 amount1) {
        // Parámetros para retirar liquidez
        INonfungiblePositionManager.DecreaseLiquidityParams memory params =
            INonfungiblePositionManager.DecreaseLiquidityParams({
                tokenId: tokenId,
                liquidity: liquidity,
                amount0Min: 0,
                amount1Min: 0,
                deadline: block.timestamp
            });

        // Retirar liquidez
        return nonfungiblePositionManager.decreaseLiquidity(params);
    }
    ```



```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@uniswap/v3-periphery/contracts/interfaces/ISwapRouter.sol";
import "@uniswap/v3-periphery/contracts/interfaces/INonfungiblePositionManager.sol";
import "@openzeppelin/contracts/token/ERC20/IERC20.sol";

contract UniswapV3Interaction {
    ISwapRouter public swapRouter;
    INonfungiblePositionManager public nonfungiblePositionManager;

    constructor(address _swapRouter, address _positionManager) {
        swapRouter = ISwapRouter(_swapRouter);
        nonfungiblePositionManager = INonfungiblePositionManager(_positionManager);
    }

    function swapExactInputSingle(
        address tokenIn,
        address tokenOut,
        uint24 fee,
        uint256 amountIn,
        address recipient
    ) external returns (uint256 amountOut) {
        IERC20(tokenIn).approve(address(swapRouter), amountIn);

        ISwapRouter.ExactInputSingleParams memory params =
            ISwapRouter.ExactInputSingleParams({
                tokenIn: tokenIn,
                tokenOut: tokenOut,
                fee: fee,
                recipient: recipient,
                deadline: block.timestamp,
                amountIn: amountIn,
                amountOutMinimum: 0,
                sqrtPriceLimitX96: 0
            });

        amountOut = swapRouter.exactInputSingle(params);
    }
    
    function addLiquidity(
        address tokenA,
        address tokenB,
        uint24 fee,
        int24 tickLower,
        int24 tickUpper,
        uint256 amountA,
        uint256 amountB,
        address recipient
    ) external returns (uint256 tokenId, uint128 liquidity, uint256 amount0, uint256 amount1) {
        IERC20(tokenA).approve(address(nonfungiblePositionManager), amountA);
        IERC20(tokenB).approve(address(nonfungiblePositionManager), amountB);

        INonfungiblePositionManager.MintParams memory params =
            INonfungiblePositionManager.MintParams({
                token0: tokenA,
                token1: tokenB,
                fee: fee,
                tickLower: tickLower,
                tickUpper: tickUpper,
                amount0Desired: amountA,
                amount1Desired: amountB,
                amount0Min: 0,
                amount1Min: 0,
                recipient: recipient,
            deadline: block.timestamp
        });

        // Añadir liquidez y recibir un NFT de posición
        return nonfungiblePositionManager.mint(params);
    }
    
    function removeLiquidity(
        uint256 tokenId,
        uint128 liquidity
    ) external returns (uint256 amount0, uint256 amount1) {
        // Parámetros para retirar liquidez
        INonfungiblePositionManager.DecreaseLiquidityParams memory params =
            INonfungiblePositionManager.DecreaseLiquidityParams({
                tokenId: tokenId,
                liquidity: liquidity,
                amount0Min: 0,
                amount1Min: 0,
                deadline: block.timestamp
            });
    
        // Retirar liquidez
        return nonfungiblePositionManager.decreaseLiquidity(params);
    }
}
```
