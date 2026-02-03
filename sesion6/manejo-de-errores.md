---
icon: square-small
---

# Manejo de Errores

El **manejo de errores** en Solidity es clave para que tus contratos funcionen de manera segura y predecible. Imagínate que estás jugando un videojuego, si tu personaje intenta saltar por un abismo y el juego no tiene una manera de lidiar con ese error, simplemente te caes al vacío y el juego se rompe. Pues en Solidity pasa algo parecido. Sin un buen manejo de errores, el contrato puede comportarse de forma inesperada y los usuarios pueden perder dinero o recursos.

### ¿Por qué es importante manejar errores?

Cuando ejecutas un contrato, muchas cosas pueden salir mal: intentas transferir más Ether del que tienes, llamas a una función con parámetros incorrectos, o hay un bug en la lógica. Si no controlas estos errores, el contrato puede comportarse de manera impredecible y causar problemas. Usar las herramientas adecuadas para manejar errores garantiza que si algo sale mal, el contrato se detiene de manera segura y devuelve el gas no utilizado.

### Herramientas para el manejo de errores en Solidity

1.  **`require`**: Verifica que se cumpla una condición antes de continuar con la ejecución. Si la condición falla, revierte la transacción, devuelve el gas no utilizado y muestra un mensaje de error. Perfecto para validar entradas de usuario o resultados de funciones.

    ```solidity
    function retirarFondos(uint monto) public {
        require(monto <= balance[msg.sender], "No tienes suficientes fondos");
        balance[msg.sender] -= monto;
    }
    ```

    Aquí, `require` se asegura de que el usuario no intente retirar más de lo que tiene. Si no se cumple la condición, el contrato se detiene y muestra el mensaje de error "No tienes suficientes fondos".
2.  **`revert`**: Similar a `require`, pero se usa para revertir transacciones en situaciones más complejas, donde no es posible evaluar la condición directamente en la misma línea. También se puede usar con un mensaje personalizado.

    ```solidity
    function transferir(address destinatario, uint monto) public {
        if (monto > balance[msg.sender]) {
            revert("Fondos insuficientes");
        }
        balance[msg.sender] -= monto;
        balance[destinatario] += monto;
    }
    ```

    Aquí, `revert` detiene la ejecución si el usuario intenta transferir más fondos de los que tiene, mostrando el mensaje "Fondos insuficientes".
3.  **`assert`**: Se utiliza para verificar condiciones internas que deberían ser siempre verdaderas. Si `assert` falla, significa que algo está muy mal en el contrato y se detiene la ejecución de inmediato sin devolver el gas utilizado.

    ```solidity
    function pruebaInmutable(uint x) public pure returns (uint) {
        assert(x != 0); // x nunca debería ser 0
        return 100 / x;
    }
    ```

    Aquí, `assert` asegura que `x` no sea 0. Si lo es, algo grave ocurre, y el contrato se detiene por completo.

### **Errores personalizados en `require` y `revert`**

Para manejar errores específicos y enviar mensajes detallados, puedes definir errores personalizados. Estos errores te permiten dar más información sobre por qué falló una operación, y son más eficientes en términos de gas.

```solidity
error FondosInsuficientes(uint solicitado, uint disponible);

function retirar(uint monto) public {
    if (monto > balance[msg.sender]) {
        revert FondosInsuficientes({
            solicitado: monto,
            disponible: balance[msg.sender]
        });
    }
    balance[msg.sender] -= monto;
}
```

En este ejemplo, si el usuario intenta retirar más de lo que tiene, se invoca el error `FondosInsuficientes`, indicando cuánto se solicitó y cuánto está disponible. Esto proporciona un nivel extra de detalle que puede ser muy útil para los usuarios.

### ¿Cuál es la diferencia entre `require`, `revert` y `assert`?

* **`require`**: Se utiliza para validar condiciones que dependen de entradas externas, como parámetros de funciones o el estado actual del contrato. Si falla, la transacción se revierte y devuelve el gas no utilizado.
* **`revert`**: Se usa para manejar condiciones más complejas donde necesitas controlar manualmente cómo y cuándo se revierte la transacción. También revierte la transacción y devuelve el gas no utilizado.
* **`assert`**: Es más drástico. Verifica condiciones internas que siempre deberían cumplirse. Si falla, es porque hay un error crítico en la lógica del contrato y no devuelve el gas utilizado.

### Ejemplo práctico: Manejo de errores en un contrato bancario

Imaginemos un contrato que permite a los usuarios depositar y retirar fondos. Si un usuario intenta retirar más de lo que tiene, queremos detener la operación y mostrar un mensaje específico.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Banco {
    mapping(address => uint) public balances;

    // Definimos un error personalizado
    error FondosInsuficientes(uint solicitado, uint disponible);

    // Función para depositar fondos
    function depositar() public payable {
        balances[msg.sender] += msg.value;
    }

    // Función para retirar fondos
    function retirar(uint monto) public {
        if (monto > balances[msg.sender]) {
            revert FondosInsuficientes(monto, balances[msg.sender]);
        }
        balances[msg.sender] -= monto;
        payable(msg.sender).transfer(monto);
    }

    // Función para verificar el balance
    function obtenerBalance() public view returns (uint) {
        return balances[msg.sender];
    }
}
```

En este contrato, si intentas retirar más fondos de los que tienes, el error `FondosInsuficientes` se activa y muestra exactamente cuánto se intentó retirar y cuánto había disponible.
