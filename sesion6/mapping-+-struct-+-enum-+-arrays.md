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

# Mapping + Struct + Enum + Arrays

¡Aquí es donde todo se junta! Combinar **mappings**, **structs**, **enums** y **arrays** te ayuda a construir una estructura compleja y súper organizada para manejar datos detallados. Con esta mezcla, puedes crear aplicaciones complejas, desde un marketplace hasta un sistema de gestión de proyectos. Cada pieza tiene su lugar y, cuando las juntas, obtienes una máquina bien engrasada que puede manejar datos de múltiples niveles y relaciones.

### ¿Cómo funciona esta combinación?

1. **Mapping**: Es como un índice que te ayuda a asociar una clave con un valor. Ideal para buscar rápidamente información específica.
2. **Struct**: Te permite agrupar datos relacionados en un solo contenedor, como el perfil de un usuario con su nombre, edad y dirección.
3. **Enum**: Define un conjunto limitado de opciones, como estados de un proyecto o niveles de acceso.
4. **Array**: Almacena una lista de elementos del mismo tipo, como un conjunto de tareas o productos.

### Ejemplo práctico: Sistema de Gestión de Proyectos

Imaginemos que quieres construir un sistema donde puedas gestionar proyectos, cada proyecto tiene diferentes tareas, cada tarea tiene un estado y cada usuario puede estar involucrado en varios proyectos. Vamos a combinar mappings, structs, enums y arrays para lograrlo.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract GestionDeProyectos {
    // Enum para los estados de una tarea
    enum EstadoTarea { Pendiente, EnProgreso, Completada, Cancelada }

    // Struct para representar una tarea
    struct Tarea {
        string descripcion;
        EstadoTarea estado;
        uint fechaCreacion;
    }

    // Struct para representar un proyecto
    struct Proyecto {
        string nombre;
        address lider;
        Tarea[] tareas;
    }

    // Mapping de usuario a una lista de proyectos
    mapping(address => Proyecto[]) proyectosPorUsuario;

    // Función para crear un nuevo proyecto
    function crearProyecto(string memory _nombre) public {
        // Creamos un proyecto nuevo con el nombre y el líder que lo crea
        Proyecto memory nuevoProyecto;
        nuevoProyecto.nombre = _nombre;
        nuevoProyecto.lider = msg.sender;
        
        // Agregamos el proyecto a la lista de proyectos del usuario
        proyectosPorUsuario[msg.sender].push(nuevoProyecto);
    }

    // Función para agregar una nueva tarea a un proyecto específico
    function agregarTarea(uint indiceProyecto, string memory _descripcion) public {
        // Creamos una nueva tarea y la agregamos al proyecto
        Tarea memory nuevaTarea = Tarea(_descripcion, EstadoTarea.Pendiente, block.timestamp);
        proyectosPorUsuario[msg.sender][indiceProyecto].tareas.push(nuevaTarea);
    }

    // Función para actualizar el estado de una tarea específica en un proyecto
    function actualizarEstadoTarea(uint indiceProyecto, uint indiceTarea, EstadoTarea nuevoEstado) public {
        // Actualizamos el estado de la tarea
        proyectosPorUsuario[msg.sender][indiceProyecto].tareas[indiceTarea].estado = nuevoEstado;
    }

    // Función para obtener los detalles de un proyecto específico
    function obtenerProyecto(address usuario, uint indiceProyecto) public view returns (string memory, address, uint) {
        Proyecto memory proyecto = proyectosPorUsuario[usuario][indiceProyecto];
        return (proyecto.nombre, proyecto.lider, proyecto.tareas.length);
    }

    // Función para obtener los detalles de una tarea específica en un proyecto
    function obtenerTarea(address usuario, uint indiceProyecto, uint indiceTarea) public view returns (string memory, EstadoTarea, uint) {
        Tarea memory tarea = proyectosPorUsuario[usuario][indiceProyecto].tareas[indiceTarea];
        return (tarea.descripcion, tarea.estado, tarea.fechaCreacion);
    }
}
```

### ¿Cómo funciona este contrato?

1. **Enum `EstadoTarea`**: Define cuatro posibles estados para cada tarea: `Pendiente`, `EnProgreso`, `Completada` y `Cancelada`.
2. **Struct `Tarea`**: Agrupa la descripción de la tarea, su estado y la fecha de creación.
3. **Struct `Proyecto`**: Agrupa el nombre del proyecto, el líder (quien lo creó) y un array de tareas (`Tarea[]`).
4. **Mapping `proyectosPorUsuario`**: Almacena un array de `Proyecto[]` para cada usuario (`address`), permitiendo que cada usuario tenga múltiples proyectos.

### Interacción con el contrato:

* Los usuarios pueden **crear proyectos** con `crearProyecto`, asignándole un nombre y guardándolo en su lista de proyectos.
* Con `agregarTarea`, puedes **agregar tareas** a un proyecto específico.
* Usando `actualizarEstadoTarea`, puedes **cambiar el estado** de una tarea, pasando de `Pendiente` a `EnProgreso`, `Completada` o `Cancelada`.
* La función `obtenerProyecto` permite **consultar detalles** de un proyecto, como su nombre, líder y número de tareas.
* Con `obtenerTarea`, puedes **consultar detalles específicos** de una tarea dentro de un proyecto, incluyendo su descripción, estado y fecha de creación.

### Ejemplo en la práctica:

Imaginemos que Bob crea un proyecto llamado "Lanzamiento de App", y añade dos tareas:

**Proyecto**: "Lanzamiento de App"

* **Tarea 1**: "Diseñar la interfaz" (Pendiente)
* **Tarea 2**: "Crear la landing page" (EnProgreso)

| **Usuario** | **Proyecto**       | **Índice Tarea** | **Descripción**       | **Estado** | **Fecha de Creación** |
| ----------- | ------------------ | ---------------- | --------------------- | ---------- | --------------------- |
| 0x456...def | Lanzamiento de App | 0                | Diseñar la interfaz   | Pendiente  | 1696015200            |
| 0x456...def | Lanzamiento de App | 1                | Crear la landing page | EnProgreso | 1696015400            |
