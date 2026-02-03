---
icon: square-small
---

# Valores por Defecto

En Solidity, cada tipo de dato tiene un **valor por defecto** cuando declaras una variable pero no la inicializas. Es como cuando compras una camiseta online y viene en "talla única" por defecto (aunque a veces eso no le queda a nadie).

Los **valores por defecto** te garantizan que tus variables no estarán vacías o "rotas" cuando las declares pero olvides inicializarlas. Solidity siempre les asignará un valor seguro para que tu contrato no se caiga por falta de datos. Así que, si no te molestaste en darle un valor inicial a algo, ¡Solidity lo hará por ti!

### ¿Cuáles son esos valores por defecto?

Aquí te va la lista rápida para que siempre sepas qué esperar cuando una variable no tiene un valor asignado:

* **uint (números enteros sin signo)**: El valor por defecto es 0. No hay números negativos, así que siempre empieza desde 0.
* **int (números enteros con signo)**: También empiezan en 0, pero aquí puedes tener tanto números positivos como negativos, aunque de inicio tendrás un 0 neutral.
* **bool (booleanos)**: Aquí el valor por defecto es `false`. Así que si no dices nada, una variable booleana siempre arranca como "mentira".
* **address (direcciones)**: Las direcciones no inicializadas serán `0x0000000000000000000000000000000000000000`. Sí, toda esa serie de ceros es el valor por defecto.
* **bytes y strings**: Estos tipos son un poco más raros. Los `bytes` y `string` vacíos tienen valores por defecto que equivalen a secuencias vacías (como un string vacío `""` o `0x` para `bytes`).

```solidity
uint256 public numero; // Por defecto será 0
bool public estado;    // Por defecto será false
address public direccion; // Por defecto será 0x0000000000000000000000000000000000000000
string public nombre; // Por defecto será ""
bytes public data; // Por defecto será 0x
```
