---
icon: square-small
---

# Constructor

El **constructor** en Solidity es ese momento inicial donde defines cómo se va a configurar todo tu contrato. Es el encargado de poner las cosas en su lugar desde el principio. Solo se ejecuta una vez, al momento de desplegar el contrato, y es perfecto para establecer variables iniciales, asignar roles, o configurar cualquier valor que no quieras cambiar después.

### ¿Qué es un constructor?

Un constructor es una función especial que tiene el mismo nombre que el contrato (en versiones antiguas de Solidity) o se declara con la palabra clave `constructor` (en versiones recientes). Se ejecuta automáticamente cuando el contrato es desplegado en la blockchain, y después de eso, desaparece como un ninja, no se puede llamar nuevamente ni actualizar.

**Sintaxis básica:**

```solidity
constructor() {
    // Lógica del constructor
}
```

Por ejemplo, si queremos asignar al creador del contrato como el "propietario", podemos hacerlo en el constructor:

```solidity
contract MiContrato {
    address public propietario;

    constructor() {
        propietario = msg.sender; // Asigna al creador del contrato como propietario
    }
}
```

En este caso, `msg.sender` se refiere a la dirección que desplegó el contrato, y el constructor la guarda como `propietario`.

### ¿Para qué se usa el constructor?

El constructor es perfecto para inicializar el estado del contrato y establecer configuraciones importantes. Algunas cosas típicas que puedes hacer en un constructor incluyen:

1. **Asignar propietarios o roles:** Ideal para contratos donde solo ciertos usuarios tienen permisos especiales, como contratos de administración.
2. **Establecer valores iniciales:** Puedes configurar límites, tarifas, o cualquier otro valor que no debería cambiar.
3. **Configurar interacciones externas:** Puedes inicializar contratos externos o configurar integraciones con otros contratos o servicios.

### Ejemplo práctico: Sistema de Registro

Vamos a construir un contrato que utiliza el constructor para establecer al propietario y un costo de registro:

```solidity
contract SistemaDeRegistro {
    address public propietario;
    uint256 public costoDeRegistro;

    // Constructor que establece el propietario y el costo de registro
    constructor(uint256 _costoDeRegistro) {
        propietario = msg.sender; // El creador del contrato es el propietario
        costoDeRegistro = _costoDeRegistro; // Establece el costo inicial
    }

    // Función para cambiar el costo de registro (solo el propietario puede hacerlo)
    function cambiarCostoDeRegistro(uint256 nuevoCosto) public {
        require(msg.sender == propietario, "Solo el propietario puede cambiar el costo.");
        costoDeRegistro = nuevoCosto;
    }
}
```

En este contrato, el constructor toma un parámetro (`_costoDeRegistro`) y lo utiliza para establecer el costo inicial de registro. También establece a `msg.sender` como el `propietario`. Después de que el contrato se despliega, nadie más puede ejecutar el constructor.

### Cosas que debes saber sobre el constructor

1. **Solo se ejecuta una vez:** Una vez que el constructor termina su ejecución, no puede ser llamado de nuevo. Es como configurar las reglas del juego: una vez que empiezas a jugar, no puedes cambiarlas.
2. **No tiene un nombre específico:** En las versiones antiguas de Solidity, el constructor debía tener el mismo nombre que el contrato. En versiones actuales, solo necesitas usar la palabra clave `constructor`.
3. **Interacciones limitadas:** Aunque puedes interactuar con otros contratos dentro del constructor, ten en cuenta que cualquier lógica que dependa de condiciones futuras debe manejarse cuidadosamente, ya que no podrás volver a ejecutar el constructor para corregir problemas.
4. **No consume gas extra:** Aunque ejecuta lógica importante, el constructor no impone costos adicionales de gas. El costo de desplegar el contrato ya incluye la ejecución del constructor.
