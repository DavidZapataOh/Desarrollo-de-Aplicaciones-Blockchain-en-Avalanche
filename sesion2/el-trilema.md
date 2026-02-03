---
icon: square-small
---

# El Trilema

El **Trilema de la Blockchain** es un término que fue popularizado por **Vitalik Buterin.** Básicamente sostiene que hay tres propiedades esenciales que una blockchain debería tener, pero que es extremadamente difícil (si no imposible) lograr las tres al mismo tiempo. Estas son:

* **Seguridad**
* **Descentralización**
* **Escalabilidad**

El dilema surge porque, en la práctica, al intentar optimizar una de estas propiedades, generalmente sacrificas una o ambas de las otras. Vamos a ver más a fondo cada una de estas:

### Seguridad

Es probablemente el aspecto más importante en cualquier blockchain. Al final del día la gente quiere saber que sus activos digitales están seguros y que la red no será vulnerable a ataques o manipulaciones. Para que una blockchain sea realmente segura, debe ser resistente a cosas como ataques del 51%, donde un atacante puede potencialmente tomar el control de la red si consigue suficiente poder computacional o participación.

En blockchains como Bitcoin y Ethereum, la seguridad está garantizada por mecanismos como **Proof of Work** o **Proof of Stake**, donde los validadores tienen que gastar recursos (ya sea energía o capital en forma de ETH) para asegurar la red.

### Descentralización

Significa que ninguna entidad o grupo tiene el control sobre la red. En una blockchain verdaderamente descentralizada, cualquier persona puede unirse como nodo o validador, y no hay una autoridad central que dicte las reglas. Esto es lo que le da a la blockchain su poder de ser resistente a la censura y de operar sin intermediarios.

El problema es que lograr un alto nivel de descentralización suele hacer más difícil escalar la red. Cuantos más nodos y validadores tienes, más tiempo y recursos pueden ser necesarios para coordinar todos esos participantes y llegar a un consenso.

### Escalabilidad

Se refiere a la capacidad de una blockchain para manejar un gran número de transacciones en un corto periodo de tiempo. Ethereum 1.0, por ejemplo, tuvo problemas con la escalabilidad, ya que solo podía procesar entre 15 y 30 transacciones por segundo. Esto puede sonar bien hasta que te das cuenta de que redes centralizadas como Visa pueden procesar miles de transacciones por segundo.

Cuando una blockchain no es escalable, se vuelve lenta y las tarifas de transacción se disparan. Este fue uno de los principales problemas que Ethereum enfrentó antes de comenzar su transición a Ethereum 2.0.

### ¿Por qué es tan complicado?

Aquí es donde entra el verdadero dilema. Mejorar una de estas tres características casi siempre implica comprometer las otras dos. Por ejemplo:

* Si intentas aumentar la **escalabilidad** a menudo sacrificas la **descentralización**. Al permitir que solo unos pocos nodos o validadores manejen la mayoría de las transacciones, pierdes parte de esa naturaleza descentralizada que hace que la blockchain sea resistente a la censura.
* Si te enfocas en **descentralización** pura, como Bitcoin, entonces es difícil escalar la red, ya que cada nodo necesita procesar y validar cada transacción individualmente, lo que puede ralentizar todo.
* Y si priorizas la **seguridad**, como ocurre en muchas blockchains, el esfuerzo y los recursos necesarios para asegurar la red pueden hacer que sea difícil escalar.

### El Trilema en Ethereum

Ethereum en sus primeras versiones, tuvo que enfrentarse a este trilema de frente. La red quería ser **segura** y **descentralizada**, pero eso llevó a problemas de **escalabilidad**, como lo vimos con las altas tarifas de gas y la congestión en la red.

Con Ethereum 2.0 y la introducción de tecnologías como **Proof of Stake** y **sharding**, la red busca una solución que mejore la **escalabilidad** sin sacrificar demasiado en términos de **seguridad** y **descentralización**. Sharding permite que la carga de trabajo se divida entre múltiples fragmentos, aumentando el número de transacciones que se pueden procesar sin tener que comprometer la descentralización de la red.



El Trilema sigue siendo un desafío sin una solución definitiva, pero muchos desarrolladores y proyectos están trabajando en cómo abordar este problema. Desde el lado de Ethereum existen las soluciones Layer 2, que veremos más adelante.
