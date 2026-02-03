---
icon: square-small
---

# Enum

Los **enum** en Solidity son listas de opciones que te permiten manejar valores predefinidos de manera más legible y organizada. Imagina que tienes una aplicación de entrega de paquetes y quieres registrar el estado del paquete como "Enviado", "En tránsito" o "Entregado". En lugar de usar números o cadenas de texto, puedes usar un `enum` para hacerlo más claro y evitar errores de lógica.

### ¿Qué es un enum?

Un `enum` (abreviación de enumeración) te permite definir un conjunto de valores posibles que una variable puede tener. Es como un menú desplegable en el que solo puedes elegir entre las opciones disponibles, evitando que ingreses valores inválidos.

**Sintaxis básica:**

```solidity
enum Estado { Enviado, EnTransito, Entregado }
```

Aquí, `Estado` es un `enum` con tres posibles valores: `Enviado`, `EnTransito` y `Entregado`. Estos valores se almacenan internamente como enteros, empezando desde 0 (Enviado = 0, EnTransito = 1, Entregado = 2).

### ¿Cómo se usan los enums?

Usar enums es súper sencillo y te permite mejorar la legibilidad del código. Por ejemplo, supongamos que queremos hacer un seguimiento del estado de un paquete:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract EnvioDePaquetes {
    // Definimos el enum para los estados del paquete
    enum Estado { Enviado, EnTransito, Entregado }

    // Variable de estado para almacenar el estado actual del paquete
    Estado public estadoActual;

    // Función para actualizar el estado del paquete
    function actualizarEstado(Estado nuevoEstado) public {
        estadoActual = nuevoEstado;
    }

    // Función para obtener el estado actual del paquete en forma de texto
    function obtenerEstado() public view returns (string memory) {
        if (estadoActual == Estado.Enviado) {
            return "El paquete ha sido enviado.";
        } else if (estadoActual == Estado.EnTransito) {
            return "El paquete está en tránsito.";
        } else {
            return "El paquete ha sido entregado.";
        }
    }
}
```

En este contrato, `estadoActual` es una variable de tipo `Estado` que solo puede tener uno de los valores predefinidos. La función `actualizarEstado` permite cambiar el estado del paquete, y `obtenerEstado` devuelve una descripción del estado actual.

### Cosas que debes saber sobre los enums

1. **Números detrás de las opciones**: Cada valor del `enum` tiene asociado un número entero empezando desde 0. Así, `Enviado` es 0, `EnTransito` es 1 y `Entregado` es 2. Esto es importante porque puedes usar estos números para comparar o asignar valores.
2. **Uso eficiente de gas**: Al ser internamente representados como números enteros, los enums son más eficientes en términos de gas que el uso de cadenas de texto para representar estados.
3. **Limitaciones de tamaño**: Un `enum` no puede tener más de 256 valores, ya que cada valor se almacena en 1 byte. Si necesitas más opciones, es mejor usar una estructura de datos diferente.
4. **Comparación directa**: Puedes comparar directamente el valor de un enum con otro valor del mismo enum. Esto hace que las decisiones de lógica basadas en el estado sean muy claras y fáciles de seguir.

### Ejemplo práctico con varios estados

Vamos a ver otro ejemplo donde usamos un enum para representar el estado de un proyecto:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Proyecto {
    // Definimos el enum para los estados del proyecto
    enum Estado { Planeacion, Desarrollo, Revision, Completado }

    // Variable de estado para almacenar el estado actual del proyecto
    Estado public estadoProyecto;

    // Función para avanzar al siguiente estado del proyecto
    function avanzarEstado() public {
        estadoProyecto = Estado(uint(estadoProyecto) + 1);
    }

    // Función para obtener el estado actual del proyecto en forma de texto
    function obtenerEstadoProyecto() public view returns (string memory) {
        if (estadoProyecto == Estado.Planeacion) {
            return "El proyecto está en fase de planeación.";
        } else if (estadoProyecto == Estado.Desarrollo) {
            return "El proyecto está en desarrollo.";
        } else if (estadoProyecto == Estado.Revision) {
            return "El proyecto está en revisión.";
        } else {
            return "El proyecto está completado.";
        }
    }
}
```

En este contrato, `estadoProyecto` pasa por cuatro estados: `Planeacion`, `Desarrollo`, `Revision` y `Completado`. La función `avanzarEstado` permite moverse al siguiente estado, siempre que no esté ya en `Completado`.
