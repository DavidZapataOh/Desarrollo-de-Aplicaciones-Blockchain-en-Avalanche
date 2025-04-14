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

# &#x20;Automated Market Makers (AMM)

Para entender cómo llegamos a los **Automated Market Makers (AMM)** y los **pools de liquidez** en las finanzas descentralizadas, es útil comenzar con un paralelo que todos conocemos, los mercados tradicionales de acciones y divisas, donde la oferta y la demanda determinan el precio de cada activo.

### Una breve historia

En un lugar aislado y escondido entre las montañas, existía una pequeña aldea llamada **Aldea de las Colinas**. Esta aldea era famosa porque sus habitantes, los **Hidros** y los **Orios**, usaban monedas distintas, los Hidros empleaban **hidromonedas** y los Orios, **oriomonedas**. Aunque ambos vivían en paz, las monedas no eran compatibles y el intercambio entre ambos grupos era un desafío que complicaba la vida de la aldea. Por años los aldeanos dependieron de un sistema de trueque informal, donde debían encontrar a alguien que necesitara justo lo que ofrecían en el momento adecuado.

**La Llegada del Puente del Mercado**

Un día, un comerciante viajero llamado **Arturo** llegó a la aldea y notó las dificultades de los aldeanos para intercambiar hidromonedas y oriomonedas. Decidido a ayudar, Arturo propuso construir un **puente del mercado** entre ambas partes de la aldea, donde los aldeanos pudieran encontrarse y comerciar con facilidad. El puente permitiría a los aldeanos realizar intercambios sin tener que buscar una contraparte exacta, utilizando un libro de órdenes para dejar constancia de sus ofertas y demandas.

Sin embargo, Arturo pronto se dio cuenta de que este sistema tenía sus problemas: encontrar coincidencias en el libro de órdenes no era fácil, y las largas filas y los retrasos hacían que los aldeanos se impacientaran. El sistema de trueque era lento y, aunque mejor que antes, la aldea todavía enfrentaba muchas limitaciones.

**La Innovación del Pozo de Liquidez**

Inspirado por el problema, Arturo tuvo una idea revolucionaria, ¿qué pasaría si él mismo creara un "pozo" donde los aldeanos pudieran **depositar sus hidromonedas y oriomonedas** para que cualquiera pudiera realizar intercambios sin necesidad de coincidencias exactas? Este sería el **Pozo de Liquidez**. Arturo explicó su idea a los aldeanos, ellos podrían dejar sus monedas en el pozo y a cambio recibirían un porcentaje de las tarifas generadas cada vez que alguien usara el pozo para hacer un intercambio.

Este sistema resultó ser un éxito. Los aldeanos comenzaron a depositar sus monedas en el pozo, y cada vez que alguien necesitaba intercambiar hidromonedas por oriomonedas, simplemente tomaba lo necesario, pagando una pequeña tarifa que se distribuía entre los proveedores de liquidez. Ahora, cualquier aldeano podía cambiar sus monedas sin esperar una coincidencia perfecta, y el puente del mercado se transformó en un lugar dinámico y eficiente.

**El Problema de la Escasez**

Todo parecía funcionar bien hasta que un día surgió un problema: **los hidros** empezaron a cruzar más al territorio de los Orios para intercambiar, y el pozo de hidromonedas comenzó a agotarse rápidamente. Los aldeanos se dieron cuenta de que, si una moneda escaseaba, los intercambios se volvían muy caros y el equilibrio se rompía. Arturo entendió que necesitaba un mecanismo que mantuviera el pozo balanceado automáticamente sin agotar una de las monedas.

Fue entonces cuando se le ocurrió un enfoque basado en un **producto constante** en lugar de una suma constante. En este sistema, conocido como **x \* y = k**, la cantidad de hidromonedas y oriomonedas siempre se multiplicaba para mantener el balance. Esto significaba que a medida que una moneda se volvía escasa, su precio aumentaba, incentivando a los aldeanos a hacer intercambios en sentido opuesto y manteniendo el equilibrio de ambos lados del pozo.

**La Aparición de los Proveedores de Liquidez**

Con el éxito del sistema de Arturo, más aldeanos querían depositar sus monedas en el pozo y ganar una parte de las tarifas. Arturo empezó a emitir **certificados de participación** a cada proveedor de liquidez, de modo que cada uno tuviera una proporción del pozo acorde con su contribución. Ahora, los aldeanos no solo intercambiaban monedas con facilidad, sino que también podían ganar un ingreso pasivo con sus depósitos.

Sin embargo, algunos aldeanos comenzaron a notar que cuando el precio de una moneda variaba demasiado rápido, su participación en el pozo se veía afectada por algo llamado **pérdida impermanente**. Aunque este fenómeno podía causar cierta desventaja, la mayoría de los aldeanos consideraba que los beneficios del pozo superaban los riesgos, y continuaron utilizando el sistema para facilitar la vida en la aldea.

**El Legado del Puente de Arturo**

Gracias a la creatividad de Arturo, el puente del mercado transformó la economía de la Aldea de las Colinas. El sistema de AMM y los liquidity pools impulsaron el comercio de hidromonedas y oriomonedas, y con el tiempo, aldeanos de otras regiones comenzaron a llegar para ver esta maravilla. Arturo había creado no solo un sistema de intercambio eficiente, sino un modelo para el futuro de los mercados descentralizados.

### ¿Qué es un Automated Market Maker (AMM)?

Los **Automated Market Makers (AMM)** son contratos inteligentes que permiten el intercambio de activos en un mercado sin depender de un libro de órdenes tradicional, como el que Arturo había creado inicialmente en la aldea. En lugar de buscar una coincidencia directa entre compradores y vendedores, los AMM utilizan **pools de liquidez** (o pozos de liquidez) donde los usuarios depositan pares de tokens. Este sistema asegura que siempre haya liquidez disponible y permite que cualquier usuario realice intercambios de manera fluida y automática.

**La Fórmula de Producto Constante: x \* y = k**

Para mantener el equilibrio entre dos monedas en el pool de liquidez, los AMM aplican la fórmula **x \* y = k**, donde "x" y "y" representan la cantidad de cada token en el pool y "k" es una constante. Esta fórmula garantiza que, a medida que la cantidad de una moneda disminuye, su precio sube, incentivando el comercio en la dirección opuesta y evitando que se agote por completo, similar a cómo Arturo ajustó los precios en el pozo de liquidez de la aldea.

**Incentivos para los Proveedores de Liquidez (LP)**

En un AMM los usuarios pueden convertirse en **proveedores de liquidez (LP)**, depositando pares de tokens en el pool a cambio de una participación en las tarifas generadas por el intercambio de esos tokens. Así como en la historia los aldeanos recibían una recompensa por sus depósitos, en los AMM los LP obtienen ingresos pasivos, lo que motiva la participación y asegura la disponibilidad constante de activos en el pool.

### Ejemplo de Intercambio AVAX/USDC

Para entender cómo funcionan los AMM en la práctica, tomemos el ejemplo de un **pool de liquidez entre AVAX y USDC**. Imagina que estamos usando un AMM en un DEX como **Pangolin** (un intercambio descentralizado que opera en la red Avalanche), donde los usuarios pueden intercambiar AVAX por USDC y viceversa.

Supongamos que alguien quiere cambiar 1 AVAX por USDC. En este caso, el DEX consulta el pool de liquidez entre AVAX y USDC, que ya tiene una cantidad de cada token depositada, por ejemplo, 1,000 AVAX y 10,000 USDC. La fórmula del AMM asegura que la relación de ambos tokens se mantenga balanceada, en este caso bajo la ecuación _**x \* y = k**_, donde _**x**_ es la cantidad de AVAX en el pool, _**y**_ es la cantidad de USDC, y _**k**_ es una constante fija. Esto significa que al agregar o retirar AVAX o USDC, el precio de cada uno cambia para mantener el equilibrio.

* **Estado Inicial**:
  * El pool contiene 1,000 AVAX y 10,000 USDC, con una constante _**k = 1,000,000**_.
  * Esto significa que el precio de 1 AVAX es 10 USDC (porque el balance actual del pool es 1,000 AVAX por 10,000 USDC).
* **Intercambio**:
  * Un usuario deposita 1 AVAX en el pool y retira una cantidad de USDC.
  * Como ahora hay 1,001 AVAX en el pool, el AMM ajusta la cantidad de USDC disponible para mantener la constante _**k**_.
  * El AMM retira una cantidad de USDC, digamos 9.90 USDC, que es menos de 10 debido a la fluctuación causada por el cambio en la relación de ambos tokens en el pool.
* **Nuevo Balance**:
  * Después del intercambio, el pool tiene 1,001 AVAX y 9,990.1 USDC.
  * Esto significa que el precio de AVAX en términos de USDC ha aumentado ligeramente, incentivando a otros usuarios a intercambiar en dirección opuesta (USDC a AVAX) para equilibrar el pool.
