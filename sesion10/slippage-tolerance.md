---
icon: square-small
---

# Slippage Tolerance

Cuando se realizan intercambios en Uniswap o en otros AMM, uno de los factores importantes a considerar es la **tolerancia al deslizamiento** (slippage tolerance). Esta es la variación en el precio aceptable para el usuario entre el momento en que se inicia la transacción y el momento en que se ejecuta. Debido a la naturaleza dinámica de los AMM, donde los precios cambian continuamente con cada transacción, la **tolerancia al deslizamiento** permite definir el máximo de diferencia de precio que un usuario está dispuesto a aceptar.

### **¿Por Qué Ocurre el Slippage?**

En un AMM, cada intercambio afecta la relación de los tokens en el pool, lo que puede modificar el precio de forma continua. Si un usuario realiza un intercambio de un token muy volátil o un intercambio grande en comparación con el tamaño del pool, es probable que experimente un cambio de precio, o **slippage**. Cuanto más grande sea el intercambio en relación con el pool de liquidez, mayor será el impacto en el precio.

Por ejemplo, si alguien quiere intercambiar **ETH por DAI** en Uniswap, cada ETH adicional que se intercambie reducirá la cantidad de DAI en el pool y aumentará su precio, haciendo que el valor recibido disminuya para el usuario.

### **¿Cómo Funciona la Tolerancia al Deslizamiento?**

La **tolerancia al deslizamiento** se define como un porcentaje de variación en el precio. Si por ejemplo un usuario establece una tolerancia del 1%, acepta recibir hasta un 1% menos de tokens de lo que el precio actual indica. Si el precio cambia más de ese 1% durante la transacción, el intercambio se cancela automáticamente para proteger al usuario de recibir menos de lo esperado. Este ajuste es fundamental en mercados con alta volatilidad o en intercambios grandes.

### **Ejemplo Práctico en Uniswap**

Imagina que un usuario desea intercambiar 10 AVAX por USDC, y la tasa actual es de 10 USDC por AVAX. Si establece una tolerancia al deslizamiento del 0.5%, eso significa que acepta recibir un mínimo de 99.5 USDC. Sin embargo, si durante la ejecución del intercambio el precio cae y la cantidad de USDC que recibiría baja a 99 USDC, el intercambio no se completará debido a que excede la tolerancia al deslizamiento establecida.

### **La Importancia de Ajustar la Tolerancia Correctamente**

Establecer la **tolerancia al deslizamiento** es un balance entre evitar pérdidas y asegurar que la transacción se ejecute:

* **Tolerancia Baja**: Protege al usuario de recibir menos de lo deseado, pero si la volatilidad es alta, la transacción podría no ejecutarse.
* **Tolerancia Alta**: Aumenta la probabilidad de que la transacción se complete, aunque con el riesgo de recibir significativamente menos de lo estimado.
