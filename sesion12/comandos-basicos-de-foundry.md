---
icon: square-small
---

# Comandos básicos de Foundry

Cuando creamos un proyecto con Foundry, este genera automáticamente un ejemplo listo para usar, el contrato **`Counter.sol`**, sus pruebas **`Counter.t.sol`** y un script de despliegue **`Counter.s.sol`**. Por ahora no los borres, los vamos a dejar tal cual para usarlos como base mientras exploramos los comandos básicos de Foundry.

## Compilar

Para compilar el proyecto ejecuta:

```bash
forge compile
```

Al finalizar, verás carpetas nuevas como `out/` y `cache/`.

* En **`out/`** Foundry guarda los artefactos de compilación: **ABI**, **bytecode**, metadata, etc.
* En **`cache/`** guarda información para acelerar compilaciones futuras.

## Testear

Para ejecutar los tests:

```bash
forge test
```

Si quieres ver más detalle (logs y trazas), usa:

```bash
forge test -vvv
```

## Desplegar

### En local (Anvil)

Primero inicia el nodo local:

```bash
anvil
```

Anvil te mostrará varias cuentas con fondos de prueba y sus llaves privadas. Para poder firmar con Cast/Foundry, importaremos una llave una sola vez.

Importa la llave en el keystore de Cast:

```bash
cast wallet import localKey --interactive
```

Te pedirá:

* **Private key**
* **Password** para cifrarla en tu máquina

> Esto se hace **una sola vez**. Después puedes reutilizar `--account localKey` sin volver a pegar la llave.

Ahora despliega usando el script:

```bash
forge script script/Counter.s.sol --rpc-url 127.0.0.1:8545 --broadcast --account localKey --sender 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266
```

Importante:

* `--broadcast` hace que el script realmente envíe las transacciones.
* `--sender` debe ser la dirección que corresponde a la llave que importaste (puede ser una de las cuentas que te imprime Anvil).

### En testnet (Fuji)

Importa la llave que usarás en Fuji:

```bash
cast wallet import testKey --interactive
```

Luego ejecuta el script apuntando al RPC de Fuji:

```bash
forge script script/Counter.s.sol --rpc-url https://api.avax-test.network/ext/bc/C/rpc --broadcast --account testKey --sender 0xtuaddress
```

> Asegúrate de tener AVAX de testnet en `0xTuAddress`, si no, la transacción fallará por falta de gas.

### En mainnet (Avalanche C-Chain)

Importa tu llave de mainnet (idealmente una wallet dedicada solo a deploys):

```bash
cast wallet import maintKey --interactive
```

Y despliega usando el RPC de mainnet:

```bash
forge script script/Counter.s.sol --rpc-url https://api.avax.network/ext/bc/C/rpc --broadcast --account testKey --sender 0xtuaddress
```

