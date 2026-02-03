---
icon: square-small
---

# Unidades de Medida del Ether

En la EVM no todo se mide en Ether como tal. Existen diferentes unidades para representar cantidades de esta criptomoneda, un poco como cuando usamos gramos, kilogramos y toneladas para medir peso. Entender estas unidades es clave para no perderse en la inmensidad de ceros y decimales que a veces acompañan las transacciones en la red. ¡Vamos a conocerlas!

### ¿Qué es Ether y por qué tiene tantas unidades?

Ether (ETH) es la criptomoneda nativa de la red Ethereum y se utiliza para pagar comisiones de gas, desplegar contratos inteligentes y mucho más. Pero como manejar cantidades muy pequeñas o muy grandes de Ether puede volverse incómodo, se crearon diferentes unidades para facilitar su uso. Cada una de estas unidades representa una fracción específica del Ether, similar a cómo un dólar tiene centavos.

{% hint style="info" %}
Aunque estemos trabajando en otra red diferente a Ethereum, como Avalanche, Polygon, o Binance Smart Chain, las cuales tienen su propio token nativo, de igual manera se sigue usando el termino Ether o ETH para referirse a las unidades de medidas.
{% endhint %}

### Principales Unidades de Medida del Ether

1.  **Wei**: Es la unidad más pequeña de Ether, como el átomo del universo blockchain. Piensa en `wei` como el "centavo" del Ether, pero en lugar de ser una centésima parte, ¡es una dieciochoava parte! Un Ether tiene exactamente `1,000,000,000,000,000,000` (un quintillón) de Wei. Básicamente, si ves un número enorme con muchos ceros, probablemente estés viendo Wei.

    **Ejemplo**: 1 ETH = 1,000,000,000,000,000,000 Wei
2.  **Gwei**: También conocido como "shannon", es la unidad más común cuando hablamos de tarifas de gas en Ethereum. 1 Gwei es igual a `1,000,000,000` Wei (mil millones). Si alguna vez has visto una tarifa de transacción en Gwei, es porque es la forma más práctica de expresar las tarifas sin usar tantos ceros.

    **Ejemplo**: 1 Gwei = 1,000,000,000 Wei
3.  **Ether**: Es la unidad principal y más conocida, utilizada para representar balances y transacciones mayores. Si alguien te dice que tiene 5 ETH, eso es 5 Ethers completos, sin ninguna subdivisión.

    **Ejemplo**: 1 Ether = 1,000,000,000,000,000,000 Wei

### Tabla Comparativa de Unidades

| **Unidad** | **Símbolo** | **Valor en Wei**          | **Descripción**       |
| ---------- | ----------- | ------------------------- | --------------------- |
| Wei        | wei         | 1                         | Unidad más pequeña    |
| Kwei       | babbage     | 1,000                     | 1,000 Wei             |
| Mwei       | lovelace    | 1,000,000                 | 1 millón de Wei       |
| Gwei       | shannon     | 1,000,000,000             | 1 mil millones de Wei |
| Microether | szabo       | 1,000,000,000,000         | 1 billón de Wei       |
| Milliether | finney      | 1,000,000,000,000,000     | 1 cuatrillón de Wei   |
| Ether      | eth         | 1,000,000,000,000,000,000 | 1 quintillón de Wei   |

### ¿Por qué tantas unidades?

Las distintas unidades son útiles para representar diferentes cantidades de Ether sin lidiar con montones de ceros. Imagina tener que expresar una transacción de 0.000000001 ETH en Wei: sería un número gigante y complicado de manejar. En su lugar, decimos 1 Gwei, y listo. Las unidades también ayudan a evitar errores, es fácil confundirse cuando estás lidiando con números como `1000000000000000000` (1 Ether en Wei).

### ¿Cuándo usar cada unidad?

1. **Wei**: Ideal para cálculos precisos y pequeños, como dividir Ether en partes extremadamente pequeñas.
2. **Gwei**: La opción más usada para tarifas de gas. Si ves tarifas como 30 Gwei, significa que cada unidad de gas cuesta 30 Gwei.
3. **Ether**: Se usa para representar cantidades completas de la moneda, como balances de cuentas o transacciones mayores.
