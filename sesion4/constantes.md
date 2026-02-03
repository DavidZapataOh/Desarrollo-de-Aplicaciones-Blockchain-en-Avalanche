---
icon: square-small
---

# Constantes

Las **constantes** en Solidity son como esas reglas que nunca cambian, tipo “no se come pizza con piña” (aunque sabemos que algunos no respetan esa constante). Son valores que, una vez definidos, no se pueden modificar, lo que las hace perfectas para datos que no deberían cambiar nunca, como direcciones importantes, límites máximos, o configuraciones fijas del contrato.

Definir constantes en tu contrato te ayuda a ahorrar gas, ya que su valor se almacena directamente en el bytecode del contrato y no ocupa espacio en la blockchain.

```solidity
uint256 public constant LIMITE_MAXIMO = 1000;
address public constant DIRECCION_TESORERIA = 0x1234567890123456789012345678901234567890;
```

Aquí, `LIMITE_MAXIMO` y `DIRECCION_TESORERIA` son constantes que no se pueden cambiar nunca. Esto es genial para valores que no deben modificarse bajo ninguna circunstancia.
