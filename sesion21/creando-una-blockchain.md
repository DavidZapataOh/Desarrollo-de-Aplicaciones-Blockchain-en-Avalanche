---
icon: square-small
---

# Creando una Blockchain

Avalanche nos facilita la creación de una Blockchain L1 mediante una herramienta web llamada el L1 Toolbox, con la cual configuraremos la blockchain según nuestras necesidades, crearemos y vinculamos los nodos validadores y lo pondremos a funcionar.&#x20;

{% embed url="https://build.avax.network/tools/l1-toolbox#createChain" %}

Para llevar a cabo este proceso es importante tener la extensión de Core instalada en tu navegador, sin ella no podrás usar la herramienta de creación de L1.

{% embed url="https://core.app/download" %}

El alta de una L1 se registra en la **P-Chain** mediante dos transacciones:

1. **CreateSubnetTx** → crea el contenedor (Subnet)
2. **CreateChainTx** → crea el **registro de la blockchain** y la asocia a esa Subnet

> Nota rápida\
> El **owner** de la Subnet solo importa al crearla. Si vas a convertirla en L1 enseguida (con permisos/parametrización propios), no necesitas un owner multisig desde el día uno.

## Pre-requisito: Conseguir Faucet

Lo primero que haremos es asegurarnos de que estamos en modo Testnet, puedes configurarlo en la esquina superior derecha de la sección Core del Toolbox.

<figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>

Necesitaremos AVAX tanto en la C-Chain como en la P-Chain para pagar las transacciones. Ya estamos acostumbrados a trabajar en la C-Chain, la cadena donde desplegamos los contratos inteligentes, pero a la hora de crear el registro de la blockchain y los validadores, lo haremos a nivel de plataforma, la P-Chain, por tal motivo necesitaremos tener AVAX en ambas chains.

<figure><img src="../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

Para conseguir este AVAX, en el Toolbox encontraremos un botón llamado "Faucet" que nos dará la cantidad suficiente para desplegar nuestra blockchain. Debes estar registrado en el Builder Hub para poder obtener el Faucet.

<figure><img src="../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

Recomiendo pedir el Faucet en C-Chain y luego hacer el "Bridge" para enviar la mitad de esos AVAX desde la C-Chain a la P-Chain.

<figure><img src="../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

Y con esto ya tendriamos el AVAX de prueba suficiente para poder crear nuestra blockchain!

<figure><img src="../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

## Paso 1: Crear Subnet

Ahora, debemos emitir una transacción `CreateSubnetTx` desde tu dirección de P-Chain. Esta transacción crea un Subnet cuyo ID es simplemente el hash de la transacción.&#x20;

La transacción solo tiene un parámetro, el owner de la Subnet. Este propietario puede convertir esta Subnet en una L1. Automáticamente se detecta tu address de P-Chain y se toma como parámetro.

<figure><img src="../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

## Paso 2: Crea la Blockchain

Una vez creado el Subnet, emite una transacción `CreateChainTx` en la P-Chain para registrar tu blockchain. Esta transacción necesita cuatro parámetros:

* `name` → nombre de la blockchain
* `subnetID` → ID del Subnet donde se añadirá la blockchain
* `vmID` → ID de la maquina virtual (capa de ejecución) de la blockchain (por ejemplo la EVM estándar o una VM modificada)
* `genesisData` → Configuración de la blockchain

Define el Subnet ID de la Subnet que acabas de crear (Se detecta automáticamente), el nombre que quieres que tenga tu blockchain, y si quieres usar la EVM estándar/uncustomized o una personalizada (en este caso usaremos la estándar).

<figure><img src="../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

Ahora, entraremos en detalle en la pestaña de Configuración:

### Chain Parameters

Ingresa los parametros básicos de tu L1, en este caso, solo nos pide ingresar que ID queremos que tenga nuestra blockchain.

<figure><img src="../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

Este ID debe ser único, no debe haber una blockchain con este mismo ID. Para ver si el ID que ingresamos está disponible, podemos ingresar al enlace de [View registered chain IDs on chainlist.org →](https://chainlist.org/)

Importante tener activada la opción "Include Testnets".

<figure><img src="../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

Y en el buscador de "Search Networks" pon el ID que quieres verificar, si no aparece nada, significa que está disponible y puedes usarlo.

<figure><img src="../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

Pero si obtienes resultados y alguna de las redes tiene el ID que deseas usar, debes buscar otro.

<figure><img src="../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

### Permissions

Acá puedes definir el control de acceso acerca que quienes pueden desplegar contratos (**Contract Deployer Allowlist**) e interactuar (**Transaction Allowlist**) en tu blockchain.

<figure><img src="../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

Puedes dejarlo abierto, o definir un grupo de admins y managers que tendrán el privilegio de otorgar los permisos sobre quien puede desplegar o interactuar con la red. Para este ejemplo, activaremos el control de acceso para desplegar contratos en la red.

<figure><img src="../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

En este caso, yo crearé 3 cuentas más en mi wallet de Core, lo dividiremos así:

* Un address para el admin
* Un address para el manager
* Un address aprobada
* Un address sin aprobar

Con esto, cuando la blockchain esté activa, verificaremos que esta configuración se aplicó correctamente.

<figure><img src="../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

Y en la configuración:

<figure><img src="../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

El **Transaction Allowlist** lo dejaremos abierto para este ejemplo.

### Tokenomics

Te permite ajustar la configuración en cuanto a los tokens que quieres crear, como se van a repartir y si quieres que sea una cantidad fija o que se pueda mintear más en un futuro.

<figure><img src="../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

En este caso nosotros mintearé 1,000,000 de tokens a la cuenta admin, que es la que tengo conectada desde Core (y es reconocida automáticamente).

En cuanto a hacer minteable el token, esto dependerá del caso de uso, tokenomics previstos y estrategias o planes que tengas a futuro. Yo lo dejaré desactivado, pero si lo activas, es necesario configurar el control de acceso, que asignará las personas con privilegios para mintear nuevos tokens.

<figure><img src="../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

### Transaction Fee & Gas

Puedes ajustar como se comportará el gas en tu L1, optando por máximo rendimiento o por mejor eficiencia.

<figure><img src="../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>

* **Gas Limit:** es el número máximo de unidades de gas que puede contener cada bloque. Define el límite de cómputo por bloque, por lo que un valor alto permite más operaciones por bloque y aumenta el rendimiento, mientras que un valor bajo reduce la capacidad y puede prevenir abusos.
* **Target Block Rate (segundos):** determina el tiempo objetivo (en segundos) entre la creación de dos bloques consecutivos. Ajusta la cadencia de producción de bloques. Por ejemplo, 2 segundos significa que la red intentará proponer un bloque cada dos segundos aproximadamente. Un valor menor reduce la latencia y aumenta la carga de la red, un valor mayor la disminuye.
* **Min Base Fee (gwei):** define la tarifa mínima en gwei que el protocolo cobrará por cada unidad de gas. El algoritmo de tarifas puede reducir la base fee cuando hay poca demanda, pero nunca caerá por debajo de este umbral. Sirve como barrera para evitar que las comisiones bajen demasiado y atraigan spam.
* **Base Fee Change Denominator:** controla la velocidad a la que se ajusta la base fee entre bloques. Cuanto mayor es este denominador, más lentamente cambian las tarifas. Por ejemplo, un denominador de 48 permite que la base fee suba o baje a un ritmo más gradual que un denominador de 8.
* **Min Block Gas Cost:** establece el valor mínimo del **coste de gas por bloque**. Es el umbral inferior que puede tener este coste al ajustar las tarifas. Un mínimo de 0 implica que el coste de gas por bloque no bajará a valores negativos.
* **Max Block Gas Cost:** fija el valor máximo que puede alcanzar el coste de gas por bloque. Impide que el protocolo eleve el coste por encima de este techo cuando la red está muy saturada.
* **Block Gas Cost Step:** indica en cuánto puede subir o bajar el coste de gas por bloque de un bloque a otro. Este “paso” de ajuste limita la variación entre bloques y suaviza los cambios bruscos.
* **Target Gas:** es la cantidad de gas que, idealmente, debería consumirse en cada bloque. Si los bloques usan más gas que este valor, la base fee aumentará para desalentar la demanda; si usan menos, la base fee disminuirá para incentivar transacciones.

Por ejemplo, imaginemos que queremos enfocar nuestra L1 en aplicaciónes de privacidad que requiera una criptografía compleja como ZK, FHE y MPC. En este caso, sería optimo subir el Gas Limit para asegurarnos de soportar las pruebas ZK, la verificación de firmas, etc. También subiré el target gas para dejar un pequeño margen y mantener estable el base fee.

<figure><img src="../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

Por ultimo, tenemos dos opciones de parámetros dinámicos. Cuando están _Disabled_, cualquier cambio requiere upgrade de red. Activarlos añade flexibilidad operativa pero puede verse un poco centralizado:

* **Dynamic Fee Parameters** → activa el precompile **FeeManager** para **ajustar tarifas sin hard-fork**.
* **Dynamic Reward Parameters** → activa el precompile **RewardManager** para **cambiar la distribución de fees** (quemar, enviar a validador, contrato, etc.).

<figure><img src="../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

### Precompile Info

Resumen de los **precompilados** disponibles y la dirección que ocuparán en tu L1:

* **Contract Deployer Allow List**: controla quién despliega contratos.
* **Native Minter:** minteo del token nativo por direcciones autorizadas.
* **Transaction Allow List**: controla quién puede enviar transacciones.
* **Fee Manager**: gestión dinámica de fees.
* **Reward Manager**: gestión dinámica de recompensas.
* **Warp Messenger**: **ICM/Warp** para mensajería **entre L1s**.

### Pre-Deployed Contracts

Infraestructura que se **incluye en el génesis**:

* **Transparent Upgradeable Proxy**: patrón proxy de OpenZeppelin.
* **Proxy Admin**: administra upgrades y ownership de proxies.
* **ICM Messenger:** contrato base para **Interchain Messaging**.
* **Wrapped Native Token**: equivalente a WAVAX para envolver el token nativo a ERC-20.
* **Safe Singleton Factory**: despliegues deterministas con `CREATE2`.
* **Multicall3**: batch de llamadas eficiente.
* **Create2Deployer**: helper para usar `CREATE2` con seguridad.

### Genesis JSON

La pestaña **View Genesis JSON** muestra el génesis que se firmará en la P-Chain:

* `config.chainId` (tu Chain ID)
* `feeConfig` (parámetros de gas y base fee)
* `warpConfig` (si activaste Warp/ICM)
* `alloc` (balances iniciales y bytecode de contratos pre-deployados)

**Límite de tamaño en P-Chain:** **64 KiB**. En tu ejemplo el aviso marca **59.45 KiB (92.9%)**. Si te acercas al límite, **desactiva** pre-deploys que no uses o reduce datos iniciales.

Despues de configurar todo y estar satisfecho con la personalización, pulsa **Create Chain**. Se emitirá la `CreateChainTx` y tu L1 quedará registrada y asociada a la Subnet.

<figure><img src="../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

Y si todo salió bien, debes recibir este mensaje:

<figure><img src="../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>
