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

# Eventos

Los **eventos** en Solidity son como esos gritos de “¡Hey, algo pasó aquí!” que te permiten comunicarte desde los contratos inteligentes hacia el exterior. Imagina que estás organizando una fiesta y quieres avisar a todos cuando alguien llega, cuando la comida está lista o cuando la música cambia. Cada uno de esos avisos es como un evento, informando a quienes están fuera del contrato sobre lo que está ocurriendo adentro.

### ¿Qué es un evento?

Un evento en Solidity es una forma de registrar datos importantes en la blockchain que pueden ser consultados más tarde sin necesidad de gastar gas. Los eventos permiten que un contrato emita mensajes que son capturados por aplicaciones descentralizadas (dApps) u otros contratos para reaccionar a cambios o acciones específicas.

```solidity
event NombreDelEvento(tipoDato indexed nombreVariable, tipoDato nombreVariable);
```

Por ejemplo, si estás gestionando una subasta y quieres avisar cuando alguien hace una nueva oferta, podrías definir un evento así:

```solidity
event NuevaOferta(address indexed postor, uint cantidad);
```

Aquí, `NuevaOferta` es el nombre del evento que registra la dirección del postor y la cantidad ofrecida. La palabra `indexed` hace que ese parámetro sea más fácil de buscar, como si fuera una etiqueta.

Para emitir un evento, simplemente necesitas llamar a su nombre y pasarle los parámetros que definiste. Es como lanzar un mensaje al aire, pero solo se escucha en la blockchain.

### **Ejemplo de uso en un contrato:**

```solidity
contract Subasta {
    // Definimos el evento para las nuevas ofertas
    event NuevaOferta(address indexed postor, uint cantidad);

    // Función para hacer una oferta en la subasta
    function hacerOferta(uint _cantidad) public {
        // Lógica para gestionar la oferta...
        
        // Emitimos el evento para notificar la nueva oferta
        emit NuevaOferta(msg.sender, _cantidad);
    }
}
```

Cada vez que alguien llama a `hacerOferta`, el contrato emite el evento `NuevaOferta`, registrando quién hizo la oferta y cuánto ofreció. Esto se guarda en los registros de la blockchain y puede ser consultado por cualquier dApp interesada en seguir la subasta.

### ¿Para qué sirven los eventos?

1. **Registro histórico:** Los eventos te permiten crear un historial de lo que sucede dentro del contrato, como si fuera un diario de todas las acciones importantes.
2. **Comunicación con dApps:** Las dApps pueden escuchar los eventos para actualizar su interfaz o realizar acciones automáticas en respuesta.
3. **Reducción de costos de gas:** Los datos almacenados en eventos no son directamente accesibles por otros contratos, pero son mucho más baratos que almacenarlos como variables de estado.

### Ejemplo práctico: Evento en un contrato de votación

Imaginemos que queremos registrar cada vez que alguien vota en una elección:

```solidity
contract Votacion {
    // Definimos el evento para registrar los votos
    event VotoEmitido(address indexed votante, string candidato);

    // Función para emitir un voto
    function emitirVoto(string memory _candidato) public {
        // Lógica para gestionar el voto...

        // Emitimos el evento para registrar el voto
        emit VotoEmitido(msg.sender, _candidato);
    }
}
```

Aquí, cada vez que alguien vota, se emite el evento `VotoEmitido` con la dirección del votante y el nombre del candidato. Estos datos no solo quedan registrados en la blockchain, sino que cualquier dApp puede usarlos para mostrar resultados en tiempo real o ejecutar lógica adicional.

### Cosas que debes saber sobre los eventos

1. **No son accesibles dentro del contrato:** Aunque los eventos quedan registrados en la blockchain, no puedes acceder a ellos desde otros contratos. Sirven más como una herramienta de comunicación externa.
2. **Límite de datos:** Los eventos tienen un límite de datos de 32 bytes por parámetro, así que no puedes enviar datos muy grandes. Si necesitas almacenar mucha información, es mejor usar almacenamiento regular en el contrato.
3. **`indexed` y su magia:** Puedes marcar hasta tres parámetros de un evento como `indexed`. Esto permite buscar y filtrar esos eventos fácilmente en la blockchain, como si fueran hashtags en redes sociales.
4. **Costos de gas:** Emitir un evento cuesta gas, pero es mucho más barato que guardar los mismos datos directamente en el contrato.
