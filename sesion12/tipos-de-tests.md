---
icon: square-small
---

# Tipos de tests

Cuando escribes contratos inteligentes, testear no es “solo ver si compila”. Estás validando lógica de negocio, seguridad, supuestos económicos y comportamiento bajo condiciones extremas. En Foundry puedes cubrir esto con varios tipos de pruebas, cada una con un propósito distinto.

## Unit tests

Validan una función o una pieza pequeña de lógica en aislamiento.&#x20;

Qué buscan:

* Que una función devuelva/actualice exactamente lo esperado.
* Que falle cuando debe fallar.
* Que respete invariantes simples (por ejemplo, “nunca puede ser negativo”).

Ejemplo típico (Counter):

* `increment()` aumenta `number` en 1.
* `setNumber(20)` deja `number == 20`.

Cuándo usarlas: <mark style="color:$danger;">**siempre.**</mark> Son la base del proyecto.

## Integration tests

Verifican que varios contratos o componentes funcionen juntos.

Qué buscan:

* Interacciones entre contratos: calls, approvals, callbacks.
* Flujos completos: “depositar → emitir tokens → retirar”.
* Integraciones con dependencias: ERC20, ERC721, routers, etc.

Ejemplo típico:

* Un contrato que recibe ERC20 y luego llama a otro contrato para contabilizar depósitos.

Cuándo usarlas: cuando hay más de un contrato o dependes de librerías/protocolos.

## Negative tests

Prueban explícitamente que el contrato revierte en escenarios inválidos.

Qué buscan:

* Que `require`/`revert` se cumplan.
* Que no existan caminos donde un atacante pueda “pasarse” validaciones.

**Ejemplos:**

* Llamar funciones `onlyOwner` desde una cuenta que no es owner.
* Intentar retirar más de lo depositado.
* Parámetros fuera de rango.

Cuándo usarlas: <mark style="color:$danger;">**siempre.**</mark> Un sistema seguro tiene tantos tests de fallo como de éxito.

## Fuzzing

En vez de probar un valor, pruebas una propiedad que debe cumplirse para muchos valores. Foundry lo hace con fuzzing (te genera valores aleatorios).

Qué buscan:

* Bugs que no aparecen con valores sencillos.
* Edge cases: 0, máximos, overflows lógicos, combinaciones raras.

Ejemplo de propiedad:

* “Después de `setNumber(x)`, el valor siempre debe ser `x`”.
* “El balance total nunca debe aumentar mágicamente”.

Cuándo usarlas: cuando la lógica depende de inputs del usuario o cálculos.

## Invariant tests

Son similares al fuzzing, pero enfocadas en reglas que deben cumplirse siempre, sin importar el orden de acciones.

Qué buscan:

* Errores de consistencia en estados complejos.
* Bugs que solo salen tras muchas operaciones encadenadas.

Ejemplos de invariantes:

* “La suma de balances debe ser igual al total supply”.
* “Ningún usuario puede retirar más de lo que depositó”.
* “El contrato nunca puede quedar con un estado imposible”.

Cuándo usarla&#x73;**:** especialmente en DeFi, protocolos con accounting, pools, vaults, etc.

## Fork tests

Permiten testear contra el estado real de una red (mainnet o testnet) haciendo un “fork” local.

Qué buscan:

* Integraciones reales con protocolos existentes.
* Comportamientos exactos de contratos externos.
* Simular escenarios usando liquidez real, holders reales, etc.

Ejemplo:

* Probar que tu contrato interactúa bien con un token real o un pool real.

Cuándo usarlas: cuando integras protocolos externos y necesitas realismo.

## Gas / performance tests

Miden cuánto gas consumen funciones críticas y detectan cambios de gas entre commits.

Qué buscan:

* Regresiones de gas (una función se volvió mucho más cara).
* Puntos calientes: loops, escrituras innecesarias, storage vs memory.

Cuándo usarlas: <mark style="color:$danger;">**siempre.**</mark> La optimización es vital.
