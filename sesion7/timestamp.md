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

# Timestamp

El **timestamp** en Solidity es como el reloj del blockchain. Te permite saber en qué momento exacto (en segundos desde el 1 de enero de 1970) se creó un bloque, se ejecutó una transacción o se hizo alguna acción específica. Es súper útil para cosas como verificar plazos, establecer límites de tiempo o ejecutar funciones solo en momentos específicos.

### ¿Qué es un timestamp?

Un timestamp es un número entero que representa el tiempo en segundos desde la medianoche del 1 de enero de 1970, también conocido como "Unix epoch". En el contexto de Solidity, el timestamp generalmente se refiere al momento en que se mina un bloque.

```solidity
uint public tiempoActual = block.timestamp;
```

Aquí, `block.timestamp` devuelve el momento exacto en que se creó el bloque en el que se está ejecutando la transacción. Esto es especialmente útil para funciones que dependen del tiempo, como contratos que tienen que desbloquear fondos después de cierta fecha o que ejecutan acciones solo en periodos específicos.

### Usos comunes del timestamp en Solidity

1.  **Verificar fechas**: Puedes usar `block.timestamp` para asegurarte de que una función solo se ejecute después de un tiempo determinado.

    ```solidity
    function liberarFondos() public {
        require(block.timestamp >= fechaLiberacion, "Los fondos aún no se pueden liberar");
        // Lógica para liberar fondos
    }
    ```
2.  **Crear temporizadores**: También puedes usar timestamps para crear temporizadores o "cooldowns" en los contratos, permitiendo que ciertas acciones solo se ejecuten después de un intervalo de tiempo.

    ```solidity
    uint public ultimaAccion;

    function realizarAccion() public {
        require(block.timestamp >= ultimaAccion + 1 days, "Debes esperar 1 día antes de realizar esta acción nuevamente");
        ultimaAccion = block.timestamp;
        // Lógica de la acción
    }
    ```
3.  **Eventos específicos**: Si quieres que un evento ocurra a una hora y fecha específicas, el timestamp es la forma de programar esta lógica.

    ```solidity
    function eventoEspecial() public {
        require(block.timestamp == fechaEspecifica, "El evento solo ocurre en una fecha específica");
        // Lógica del evento especial
    }
    ```

### Cosas a tener en cuenta con los timestamps

1. **No son 100% precisos**: El timestamp es fijado por el minero que mina el bloque, y tiene un margen de manipulación de unos pocos segundos. Aunque no suele ser un problema para la mayoría de las aplicaciones, es importante tener en cuenta que no debes usar timestamps para cosas que requieran una precisión absoluta.
2. **No uses timestamps para generar números aleatorios**: Dado que los mineros pueden influir en el valor del timestamp, usarlo para generar números aleatorios en el contrato puede llevar a resultados manipulables y poco seguros.
3. **Conversiones de tiempo**: Solidity no tiene funciones de fecha y hora como las bibliotecas estándar de programación, por lo que tendrás que hacer todas las conversiones a mano (segundos, minutos, horas, días).

### Ejemplo práctico: Contrato de Subasta con Timestamp

Vamos a ver cómo se usa un timestamp en un contrato de subasta simple. La subasta solo permite pujas durante un periodo de tiempo específico:

```solidity
solidityCopy codecontract Subasta {
    address public mayorPostor;
    uint public mayorOferta;
    uint public inicioSubasta;
    uint public finSubasta;

    constructor(uint _duracionSubasta) {
        inicioSubasta = block.timestamp;
        finSubasta = inicioSubasta + _duracionSubasta;
    }

    function pujar() public payable {
        require(block.timestamp >= inicioSubasta, "La subasta no ha comenzado");
        require(block.timestamp <= finSubasta, "La subasta ha terminado");
        require(msg.value > mayorOferta, "Tu oferta debe ser mayor que la oferta actual");

        if (mayorPostor != address(0)) {
            payable(mayorPostor).transfer(mayorOferta); // Reembolsa al mayor postor anterior
        }

        mayorPostor = msg.sender;
        mayorOferta = msg.value;
    }

    function reclamarFondos() public {
        require(block.timestamp > finSubasta, "La subasta aún no ha terminado");
        require(msg.sender == mayorPostor, "Solo el mayor postor puede reclamar los fondos");
        payable(mayorPostor).transfer(mayorOferta);
    }
}
```

En este contrato de subasta:

1. **Constructor**: Define el tiempo de inicio y fin de la subasta.
2. **Función `pujar`**: Solo permite pujas durante el tiempo de la subasta.
3. **Función `reclamarFondos`**: Permite al ganador de la subasta reclamar los fondos después de que la subasta haya terminado.
