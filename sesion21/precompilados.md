---
icon: square-small
---

# Precompilados

Los precompilados son funciones de bajo nivel que viven dentro de la maquina virtual y que ejecutan un conjunto predefinido de instrucciones directamente en el cliente, sin necesidad de pasar por el proceso completo de compilación y ejecución de un contrato inteligente. Acá es donde entra en juego el segundo tipo de personalización, la modificación de la maquina virtual.

Esto significa que en lugar de implementar una lógica desde cero en Solidity (o cualquier otro lenguaje), puedes llamar a un precompilado y obtener una ejecución más rápida y eficiente, ideal para operaciones complejas como funciones criptografía.

## ¿Dónde viven los precompilados?

En una blockchain EVM los precompilados están asociados a direcciones especificas, normalmente desde 0x1 hasta 0x9. Ejemplos tipicos en Ethereum y redes compatibles incluyen funciones para:

* SHA256
* RIPEMD160
* Ecrecover
* Modular exponentiation

## ¿Cómo se usan?

Para interactuar con un precompilado:

1. Definimos una **interfaz en Solidity** que represente la función expuesta por el precompilado.
2. Usamos la dirección correspondiente como si fuera un contrato
3. Invocamos la función directamente, pasando los parámetros requeridos

Esto nos permite escribir codigo legible en Solidity, pero que en ejecución invoca directamente la lógica optimizada en Go.

Ejemplo en Solidity llamando al precompilado de SHA256:

```solidity
interface ISHA256 {
    function hashWithSHA256(string memory value) external view returns (bytes32 hash);
}

contract MyContract {
    ISHA256 mySHA256Precompile = ISHA256(0x0300000000000000000000000000000000000001);

    function doSomething() public {
        bytes32 hash = mySHA256Precompile.hashWithSHA256("test");
    }
}

```

Implementación en Go (lógica del precompilado):

```go
func hashWithSHA256(accessibleState contract.AccessibleState, caller common.Address, addr common.Address, input []byte, suppliedGas uint64, readOnly bool) (ret []byte, remainingGas uint64, err error) {
    // Lógica de gas y parseo de entrada
    // ...

    // Cálculo SHA256
    var output [32]byte = sha256.Sum256([]byte(inputStruct))

    // Empaquetado y retorno
    packedOutput, err := PackHashWithSHA256Output(output)
    if err != nil {
        return nil, remainingGas, err
    }
    return packedOutput, remainingGas, nil
}

```

En Avalanche, puedes **modificar o añadir precompilados propios** dentro de una VM personalizada. Esto permite:

* Ampliar capacidades criptográficas.
* Añadir operaciones específicas de negocio.
* Optimizar funciones críticas para tu caso de uso.

Al ser parte de la **modificación de VM**, esta opción requiere conocimientos de Go y de la arquitectura interna del cliente.
