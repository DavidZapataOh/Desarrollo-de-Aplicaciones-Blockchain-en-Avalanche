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

# Uniswap

Uniswap es uno de los proyectos fundamentales que impulsó el crecimiento de las finanzas descentralizadas (DeFi). Lanzado en 2018 por Hayden Adams, Uniswap introdujo un modelo de intercambio sin precedentes, permitiendo a los usuarios comerciar criptomonedas sin intermediarios ni la necesidad de un libro de órdenes tradicional. Este enfoque innovador transformó la forma en que se realizan los intercambios en la blockchain y estableció las bases de lo que hoy se conoce como los **Automated Market Makers (AMM)**.

### **¿Cómo Funciona Uniswap?**

Uniswap utiliza un modelo de AMM basado en una fórmula de **producto constante (x \* y = k)**, que asegura la liquidez constante en cada par de activos en el pool. En este modelo, los usuarios depositan pares de tokens (por ejemplo, ETH y USDC) en el **pool de liquidez** y a cambio reciben comisiones generadas por cada transacción en ese pool.

### **La Importancia de los Proveedores de Liquidez (LP) en Uniswap**

Uniswap funciona gracias a la participación de los **proveedores de liquidez** (LP), quienes depositan sus tokens en los pools para facilitar los intercambios. A cambio, estos proveedores reciben una parte de las comisiones de cada intercambio, lo cual crea un incentivo financiero que asegura la disponibilidad constante de activos en el DEX. Los LP obtienen "tokens de participación" que representan su proporción del pool, y estos tokens pueden ser retirados en cualquier momento, junto con las comisiones acumuladas.

### **Uniswap V2 y V3: Innovaciones en el Modelo de AMM**

A lo largo de los años, Uniswap ha evolucionado con actualizaciones significativas:

1. **Uniswap V2**: Lanzado en 2020, V2 permitió realizar intercambios directos entre cualquier par de tokens ERC-20, sin pasar por ETH como intermediario. Además, introdujo **oráculos de precio** que mejoraron la precisión de los precios en los pools.
2. **Uniswap V3**: La versión V3 introdujo el concepto de **liquidez concentrada**, permitiendo a los LP depositar liquidez en rangos de precios específicos. Esta mejora aumentó la eficiencia del capital, ya que los LP podían asignar su liquidez de manera más estratégica, maximizando los retornos en áreas de precio donde ocurren la mayoría de los intercambios.

### **Uniswap y el Ecosistema DeFi**

Uniswap ha sido una pieza fundamental en el ecosistema DeFi. Su modelo de AMM ha servido de inspiración para numerosos protocolos DeFi, como SushiSwap y PancakeSwap, y ha permitido que cualquiera pueda intercambiar tokens directamente desde su wallet, sin necesidad de un intermediario central. Esto ha democratizado el acceso al comercio de activos digitales, proporcionando un nivel de transparencia y descentralización que no se encuentra en los exchanges centralizados.

Además, al eliminar los requisitos de verificación de identidad (KYC) y proporcionar acceso global a los servicios financieros, Uniswap ha permitido que personas de todo el mundo participen en el ecosistema DeFi. La estructura sin permisos de Uniswap también ha fomentado la creación de nuevos proyectos y tokens, que pueden ser listados directamente en la plataforma sin la intervención de un intermediario.

### **Un Ejemplo de Intercambio en Uniswap: ETH y DAI**

Imaginemos que un usuario desea intercambiar **ETH por DAI** en Uniswap. Para hacerlo, el usuario deposita ETH en el pool ETH/DAI y recibe DAI a cambio, según la cantidad de cada token en el pool en ese momento. La fórmula de producto constante (x \* y = k) asegura que el precio de ETH en términos de DAI aumentará a medida que más ETH se retire del pool y se agregue más DAI. Esto crea un ajuste de precios dinámico que refleja la oferta y la demanda en tiempo real.

Cada intercambio incluye una tarifa (0.3% en V2 y configuraciones variables en V3), la cual se distribuye entre los LP que han contribuido al pool ETH/DAI, incentivando así la participación continua de liquidez en la plataforma.
