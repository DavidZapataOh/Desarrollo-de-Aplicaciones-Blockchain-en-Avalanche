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

# Condicionales If / Else

Las **condicionales `if / else`** en Solidity son estructuras de control que permiten ejecutar diferentes bloques de código dependiendo de si una condición se cumple o no. Básicamente, son el "si pasa esto, haz esto otro, si no, haz aquello" de la programación.

### ¿Cómo funciona?

En pocas palabras, `if` evalúa una condición. Si esa condición es verdadera, ejecuta el bloque de código correspondiente. Si no, puedes agregar un `else` para indicarle al contrato qué hacer en caso contrario. Vamos con ejemplos para que quede más claro.

**Ejemplo básico de `if`:**

```solidity
function verificarNumero(uint256 numero) public pure returns (string memory) {
    if (numero > 10) {
        return "El número es mayor que 10";
    }
    // No hay else aquí, así que si la condición no se cumple, no pasa nada.
}
```

En este caso, la función verifica si el número es mayor que 10. Si lo es, devuelve el mensaje "El número es mayor que 10". Si no lo es, simplemente no hace nada (o puedes agregar un `else` si quieres manejar esa situación).

### ¿Y si quiero agregar más opciones?

Si necesitas controlar más de una condición, puedes usar `else` o incluso `else if` para verificar múltiples escenarios. Esto te permite manejar varias posibilidades sin complicarte la vida.

**Ejemplo de `if/else`:**

```solidity
function verificarEdad(uint256 edad) public pure returns (string memory) {
    if (edad >= 18) {
        return "Eres mayor de edad";
    } else {
        return "Eres menor de edad";
    }
}
```

Aquí la función devuelve si alguien es mayor o menor de edad, dependiendo del valor de `edad`. Pero si quieres manejar más opciones, usa `else if`.

**Ejemplo con `else if`:**

```solidity
function verificarPuntuacion(uint256 puntos) public pure returns (string memory) {
    if (puntos > 100) {
        return "Ganaste el premio mayor";
    } else if (puntos > 50) {
        return "Te llevas el segundo premio";
    } else {
        return "Sigue participando";
    }
}
```

Con `else if`, estás agregando una condición adicional. Si no ganas el premio mayor pero tienes más de 50 puntos, ¡aún te llevas algo!
