---
icon: square-small
---

# Ciclos For y While

Los **ciclos for y while** se usan para repetir un bloque de código varias veces, pero ojo, no son tan amigables con el gas. Aquí te explico cómo funcionan, cuándo usarlos (y cuándo no), y te doy algunos tips para que no termines gastando más gas del necesario.

### Ciclo `for`

El ciclo `for` es ideal para cuando sabes exactamente cuántas veces quieres que se repita algo. Es como decir: "Voy a iterar sobre estos 10 elementos y listo".

```solidity
function sumarElementos(uint[] memory numeros) public pure returns (uint) {
    uint suma = 0;
    for (uint i = 0; i < numeros.length; i++) {
        suma += numeros[i];
    }
    return suma;
}
```

En este ejemplo, `for` recorre todos los elementos de la lista `numeros` y suma cada uno a la variable `suma`. Fácil, ¿no? Pero cuidado, si el array es demasiado largo el costo de gas puede dispararse. Así que antes de usar `for` asegúrate de que el tamaño de la lista no sea un misterio.

### Ciclo `while`

El ciclo `while` repite un bloque de código mientras una condición sea verdadera. Es como decir: "Voy a seguir comiendo pizza hasta que ya no pueda más".

**Ejemplo básico:**

```solidity
function cuentaRegresiva(uint inicio) public pure returns (uint) {
    uint contador = inicio;
    while (contador > 0) {
        contador--;
    }
    return contador;
}
```

Aquí, `while` sigue restando 1 a `contador` hasta que llegue a 0. Útil, pero si no tienes cuidado con la condición, podrías caer en un loop infinito y acabar con todo el gas de la transacción.

### ¿Cuándo usarlos y cuándo evitar?

1. **No abuses**: Los ciclos son útiles, pero cada iteración consume gas. Si tu ciclo depende del input del usuario (como un array de longitud desconocida), podrías acabar con una transacción que cuesta una fortuna o que, simplemente, no se ejecuta porque se queda sin gas.
2. **Prefiere `for` sobre `while`**: En general, el ciclo `for` es más seguro porque su condición de salida suele ser más controlada. Con `while`, si te olvidas de actualizar la condición, boom, loop infinito.
3. **Considera dividir la lógica**: Si necesitas recorrer un array gigante, piensa en dividir la tarea en varias transacciones o usar eventos para notificar progreso. No es tan sencillo como un ciclo, pero te puede salvar de muchos dolores de cabeza.

### Pro Tip: Evita usar ciclos dentro de funciones de pago

Los ciclos pueden aumentar mucho el gas de una transacción. Si tu función también recibe Ether (`payable`), no es una buena idea meterle ciclos largos. La transacción puede fallar y el usuario se queda con cara de "¿qué pasó aquí?".
