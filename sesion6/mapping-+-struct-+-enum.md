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

# Mapping + Struct + Enum

¡Vamos a combinar lo mejor de tres mundos! Cuando usas **mappings**, **structs** y **enums** juntos en Solidity, puedes organizar datos súper complejos de manera ordenada y eficiente. Es como armar un rompecabezas donde cada pieza tiene su lugar y propósito. Esta combinación es ideal para aplicaciones que necesitan gestionar datos con múltiples niveles de información y lógica.

### ¿Cómo funciona la combinación?

1. **Mapping**: Te ayuda a asociar claves con valores. Puede ser un usuario con su información, un producto con su precio, o cualquier otra combinación de datos.
2. **Struct**: Agrupa diferentes tipos de datos en un solo contenedor. Piensa en un perfil de usuario que tiene nombre, edad y dirección, todo en un solo “paquete”.
3. **Enum**: Define un conjunto de opciones predefinidas, como estados de un contrato (Activo, Inactivo, Suspendido) o niveles de acceso (Usuario, Administrador).

### Ejemplo práctico: Gestión de Tareas

Imaginemos que queremos crear un sistema para gestionar tareas, donde cada tarea tiene un estado y está asignada a un usuario. Vamos a usar un `enum` para definir el estado de la tarea, un `struct` para almacenar los detalles de la tarea, y un `mapping` para organizar todas las tareas por usuario.

<pre class="language-solidity"><code class="lang-solidity">// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;
<strong>
</strong><strong>contract GestionDeTareas {
</strong>    // Definimos el enum para los estados de una tarea
    enum EstadoTarea { Pendiente, EnProgreso, Completada }

    // Creamos una struct para representar una tarea
    struct Tarea {
        string descripcion;
        EstadoTarea estado;
        uint fechaCreacion;
    }

    // Mapping de usuario a una lista de tareas
    mapping(address => Tarea[]) tareasPorUsuario;

    // Función para crear una nueva tarea
    function crearTarea(string memory _descripcion) public {
        Tarea memory nuevaTarea = Tarea(_descripcion, EstadoTarea.Pendiente, block.timestamp);
        tareasPorUsuario[msg.sender].push(nuevaTarea);
    }

    // Función para actualizar el estado de una tarea específica
    function actualizarEstadoTarea(uint indice, EstadoTarea nuevoEstado) public {
        require(indice &#x3C; tareasPorUsuario[msg.sender].length, "Indice de tarea fuera de rango");
        tareasPorUsuario[msg.sender][indice].estado = nuevoEstado;
    }

    // Función para obtener los detalles de una tarea específica
    function obtenerTarea(address usuario, uint indice) public view returns (string memory, EstadoTarea, uint) {
        Tarea memory tarea = tareasPorUsuario[usuario][indice];
        return (tarea.descripcion, tarea.estado, tarea.fechaCreacion);
    }
}
</code></pre>

1. **Enum `EstadoTarea`**: Define tres posibles estados para cada tarea: `Pendiente`, `EnProgreso` y `Completada`.
2. **Struct `Tarea`**: Agrupa la descripción de la tarea, su estado y la fecha de creación en un solo paquete.
3. **Mapping `tareasPorUsuario`**: Asocia cada dirección de usuario (`address`) con un array de structs `Tarea`, permitiendo que cada usuario tenga su propia lista de tareas.

### Interacción con el contrato:

* Los usuarios pueden **crear tareas** con `crearTarea`, lo que añade una nueva tarea a su lista.
* Pueden **actualizar el estado** de una tarea específica con `actualizarEstadoTarea`, cambiando su estado a `EnProgreso` o `Completada`.
* La función `obtenerTarea` permite **consultar los detalles** de una tarea específica de cualquier usuario, devolviendo su descripción, estado y fecha de creación.

### Ejemplo en la práctica:

Supongamos que Alice crea dos tareas y las gestiona de la siguiente manera:

1. **Crear tarea**:
   * `descripcion`: "Comprar suministros"
   * `estado`: `Pendiente`
   * `fechaCreacion`: `1696015200` (timestamp)
2. **Actualizar estado**:
   * Tarea 1: Cambia a `EnProgreso`.
   * Tarea 2: Cambia a `Completada`.

Después de estas operaciones, la estructura de datos en el mapping `tareasPorUsuario` para Alice se vería algo así:

| **Usuario** | **Índice** | **Descripción**     | **Estado** | **Fecha de Creación** |
| ----------- | ---------- | ------------------- | ---------- | --------------------- |
| 0x123...abc | 0          | Comprar suministros | EnProgreso | 1696015200            |
| 0x123...abc | 1          | Entregar informes   | Completada | 1696015300            |
