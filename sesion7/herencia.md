---
icon: square-small
---

# Herencia

La **herencia** en Solidity es como el “legado” que un contrato deja a otro. Imagina que tienes un contrato base con una serie de funciones y datos, y luego creas otro contrato que hereda todo ese contenido, añadiendo sus propias funciones y datos. Esto te permite reutilizar código, hacer contratos más organizados y hasta crear estructuras más complejas con varias capas de funcionalidades.

### ¿Qué es la herencia?

La herencia en Solidity permite que un contrato "hijo" herede las propiedades y funciones de un contrato "padre". Es como cuando heredas el talento para cocinar de tu abuela, pero luego le agregas tu toque personal. En términos técnicos, el contrato hijo puede utilizar funciones y variables del contrato padre, y también puede modificarlas o extenderlas.

**Sintaxis básica:**

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Padre {
    // Funciones y variables del contrato padre
}

contract Hijo is Padre {
    // Funciones y variables adicionales del contrato hijo
}
```

En este ejemplo, el contrato `Hijo` hereda todo el contenido de `Padre`, y también puede tener su propia lógica.

### Ejemplo práctico: Contrato Base y Contrato Heredado

Supongamos que tenemos un contrato base que maneja una lista de productos, y queremos crear un contrato heredado que gestione una tienda con esos productos:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

// Contrato base que define productos
contract Productos {
    struct Producto {
        string nombre;
        uint precio;
    }

    Producto[] public listaProductos;

    // Función para agregar productos a la lista
    function agregarProducto(string memory _nombre, uint _precio) public {
        listaProductos.push(Producto(_nombre, _precio));
    }

    // Función para obtener el número de productos
    function obtenerNumeroDeProductos() public view returns (uint) {
        return listaProductos.length;
    }
}

// Contrato que hereda de Productos y añade funcionalidad de tienda
contract Tienda is Productos {
    mapping(address => mapping(uint => uint)) public carrito;

    // Función para agregar un producto al carrito
    function agregarAlCarrito(uint _indiceProducto, uint _cantidad) public {
        require(_indiceProducto < listaProductos.length, "Producto no existe");
        carrito[msg.sender][_indiceProducto] += _cantidad;
    }

    // Función para ver el carrito de un usuario
    function verCarrito(address _usuario, uint _indiceProducto) public view returns (uint) {
        return carrito[_usuario][_indiceProducto];
    }
}
```

#### ¿Cómo funciona este contrato?

1. **Contrato `Productos`**: Define un `struct` para los productos y funciones básicas para agregar y contar productos. Este contrato actúa como la base que contiene la lista de productos.
2. **Contrato `Tienda`**: Hereda todo el contenido de `Productos` y añade funcionalidad adicional, como un carrito de compras que se gestiona con un mapping doble (`carrito`). Este mapping almacena la cantidad de productos que cada usuario tiene en su carrito.

### Ventajas de usar herencia

1. **Reutilización de código**: Puedes evitar duplicar funciones y datos comunes en varios contratos, lo que hace tu código más limpio y fácil de mantener.
2. **Modularidad**: Puedes construir funcionalidades complejas por capas, donde cada contrato añade o modifica comportamientos específicos.
3. **Facilidad de expansión**: Si necesitas agregar nuevas características, simplemente puedes crear un nuevo contrato que herede de otro, sin necesidad de modificar el contrato base.

### Palabra clave `super`

Si alguna vez necesitas que una función en el contrato hijo llame a la misma función en el contrato padre, puedes usar la palabra clave `super`. Esto es útil cuando quieres extender el comportamiento de una función en lugar de reemplazarlo por completo.

Para que una función pueda ser llamada o modificada en un contrato hijo, debe estar marcada como `virtual` en el contrato padre, y luego como `override` en el contrato hijo.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Padre {
    function decirHola() public pure virtual returns (string memory) {
        return "Hola desde el contrato padre!";
    }
}

contract Hijo is Padre {
    function decirHola() public pure override returns (string memory) {
        return string(abi.encodePacked(super.decirHola(), " Y hola desde el contrato hijo!"));
    }
}
```

En este ejemplo, `decirHola` en el contrato hijo llama a `decirHola` del contrato padre usando `super`, y luego añade su propio mensaje. El resultado es una combinación de ambos saludos.

### Herencia múltiple

Solidity también permite herencia múltiple, lo que significa que un contrato puede heredar de varios contratos a la vez. Esto suena genial, pero hay que tener cuidado con algo llamado el "Problema del Diamante", donde varios contratos padres pueden tener la misma función, lo que crea ambigüedad. Solidity maneja esto usando un orden de linealización que define qué contrato se prioriza.

<pre class="language-solidity"><code class="lang-solidity">// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;
<strong>
</strong><strong>contract A {
</strong>    function foo() public pure virtual returns (string memory) {
        return "A";
    }
}

contract B is A {
    function foo() public pure virtual override returns (string memory) {
        return "B";
    }
}

contract C is A {
    function foo() public pure virtual override returns (string memory) {
        return "C";
    }
}

contract D is B, C {
    function foo() public pure override(B, C) returns (string memory) {
        return super.foo(); // Llama a foo() de C porque C está al final del orden de herencia
    }
}
</code></pre>

En este ejemplo, el contrato `D` hereda tanto de `B` como de `C`, pero `foo` en `D` llama a la implementación de `C` debido al orden de linealización.

### ¿Qué pasa cuando hay un constructor?

Si el contrato padre tiene un constructor con parámetros, debes pasar esos parámetros desde el constructor del contrato hijo. Esto asegura que el contrato padre se inicialice correctamente antes de que el hijo comience a ejecutar su lógica.

Supongamos que tienes un contrato padre con un constructor que inicializa una variable `nombre`:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Padre {
    string public nombre;

    constructor(string memory _nombre) {
        nombre = _nombre;
    }
}

contract Hijo is Padre {
    uint8 public edad;

    // Constructor del contrato hijo, que llama al constructor del padre
    constructor(string memory _nombre, uint8 _edad) Padre(_nombre) {
        edad = _edad;
    }
}
```

En este ejemplo:

* El contrato `Padre` tiene un constructor que recibe un string `_nombre`.
* El contrato `Hijo` hereda de `Padre` y también tiene su propio constructor, que recibe un string `_nombre` y un uint `_edad`.
* En la línea `Padre(_nombre)`, el constructor del contrato `Hijo` llama al constructor del contrato `Padre`, asegurando que el `nombre` se inicialice correctamente antes de que el contrato `Hijo` establezca su propia variable `edad`.

### Herencia múltiple con constructores

Si un contrato hereda de varios contratos padres que tienen constructores, debes especificar cómo llamar a cada uno de ellos. Veamos un ejemplo:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract A {
    uint8 public x;

    constructor(uint8 _x) {
        x = _x;
    }
}

contract B {
    uint8 public y;

    constructor(uint8 _y) {
        y = _y;
    }
}

contract C is A, B {
    // Llama a los constructores de A y B
    constructor(uint8 _x, uint8 _y) A(_x) B(_y) {}
}
```

En este caso, el contrato `C` hereda de `A` y `B`, ambos con constructores que requieren parámetros. El constructor de `C` especifica cómo llamar a cada uno de ellos: `A(_x)` y `B(_y)`. Esto asegura que ambos contratos padres se inicialicen correctamente antes de que `C` continúe.

