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

# Arrays

Los **arrays** en Solidity son listas donde puedes almacenar colecciones de datos del mismo tipo. Imagina una fila de casilleros numerados, donde cada casillero puede contener un valor específico. Ya sea que necesites almacenar un grupo de números, direcciones, o cualquier otro tipo de dato, los arrays te permiten hacerlo de manera ordenada y accesible.

### ¿Qué es un array?

Un array es una estructura de datos que almacena una colección de elementos del mismo tipo, ya sea de tamaño fijo o dinámico. Cada elemento tiene un índice, comenzando desde 0, que te permite acceder o modificar su valor fácilmente.

**Sintaxis básica:**

```solidity
tipoDato[] public nombreDelArray;
```

Por ejemplo:

```solidity
uint[] public numeros;
address[] public direcciones;
```

En este caso, `numeros` es un array de números enteros (`uint`), mientras que `direcciones` es un array de direcciones (`address`). Ambos son arrays dinámicos, lo que significa que pueden crecer o disminuir de tamaño según se vayan agregando o eliminando elementos.

### Arrays de tamaño fijo y dinámico

* **Array de tamaño fijo:** Tiene un número específico de elementos que no puede cambiar una vez definido.

```solidity
uint[3] public top3Numeros = [1, 2, 3]; // Array con 3 elementos fijos
```

* **Array dinámico:** No tiene un límite predefinido y su tamaño puede cambiar agregando o eliminando elementos.

```solidity
uint[] public listaDeNumeros; // Array dinámico
```

### Operaciones básicas con arrays

Los arrays en Solidity permiten realizar operaciones comunes como agregar, modificar, eliminar y consultar elementos. Vamos a ver algunos ejemplos:

**1. Agregar elementos a un array dinámico:**

```solidity
listaDeNumeros.push(10); // Agrega el número 10 al final del array
```

**2. Acceder y modificar elementos:**

```solidity
uint primerNumero = listaDeNumeros[0]; // Accede al primer elemento (índice 0)
listaDeNumeros[0] = 20; // Cambia el valor del primer elemento a 20
```

**3. Eliminar elementos (solo para arrays dinámicos):**

```solidity
listaDeNumeros.pop(); // Elimina el último elemento del array
```

**4. Longitud del array:**

```solidity
uint longitud = listaDeNumeros.length; // Devuelve la cantidad de elementos en el array
```

### Ejemplo práctico: Lista de Participantes

Vamos a ver un ejemplo donde usamos un array dinámico para gestionar una lista de participantes en un contrato de eventos:

<pre class="language-solidity"><code class="lang-solidity">// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;
<strong>
</strong><strong>contract Evento {
</strong>    // Array dinámico de direcciones
    address[] public participantes;

    // Función para agregar un participante
    function agregarParticipante(address _participante) public {
        participantes.push(_participante);
    }

    // Función para obtener el número total de participantes
    function totalParticipantes() public view returns (uint) {
        return participantes.length;
    }

    // Función para obtener un participante por su índice
    function obtenerParticipante(uint indice) public view returns (address) {
        return participantes[indice];
    }
}
</code></pre>

En este contrato puedes agregar direcciones de participantes con `agregarParticipante`, consultar cuántos participantes hay con `totalParticipantes` y obtener un participante específico con `obtenerParticipante`.

### Cosas a tener en cuenta con los arrays

1. **Cuidado con los índices:** Siempre asegúrate de que el índice esté dentro del rango del array. Intentar acceder a un índice fuera del rango resultará en un error y fallará la transacción.
2. **Uso de gas:** Operaciones como `push` y `pop` en arrays dinámicos consumen gas. Manipular arrays grandes puede volverse costoso rápidamente, así que úsalos con moderación.
3. **No hay métodos nativos de eliminación:** Aunque puedes usar `.pop()` para eliminar el último elemento, no hay un método nativo para eliminar un elemento específico y mantener el orden. Para eliminar elementos intermedios, necesitas una lógica personalizada.
