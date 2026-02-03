---
icon: square-small
---

# Mapping

Los **mappings** son como diccionarios que te permiten almacenar pares de clave-valor de manera súper eficiente. Imagínate un gran cajón con muchas etiquetas (claves) y cada etiqueta tiene un compartimento donde guardas un dato específico (valor). Esto es básicamente lo que hacen los mappings, te permiten buscar y almacenar datos de una manera rápida y sencilla.

### ¿Qué es un mapping?

Un `mapping` en Solidity es una estructura de datos que asocia claves con valores, como una lista de contactos donde la clave es el nombre y el valor es el número de teléfono. La sintaxis es:

```solidity
mapping(tipoClave => tipoValor) public nombreDelMapping;
```

Por ejemplo:

```solidity
mapping(address => uint256) public balances;
```

En este caso, el `mapping` `balances` asocia direcciones (`address`) con números enteros (`uint256`). Así cada dirección tiene un saldo asociado que se puede actualizar o consultar fácilmente.

### ¿Cómo funcionan los mappings?

Lo interesante de los mappings es que **cada clave siempre existe**, pero si nunca se ha asignado un valor, devolverá el valor por defecto del tipo de dato correspondiente (por ejemplo, `0` para enteros, `false` para booleanos, etc.). Así que si consultas un `mapping` con una clave que nunca has usado antes, no te va a dar un error, sino que te va a decir algo como "bueno, aún no hay datos aquí, pero si quieres puedo empezar a guardar lo que me digas".

### Ejemplo básico:

<pre class="language-solidity"><code class="lang-solidity">// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;
<strong>
</strong><strong>contract Invitaciones {
</strong>    // Creamos un mapping para invitar usuarios a fiesta
    mapping(address => bool) invitados;

    // Función para invitar a un usuario
    function invitar(address usuario) public {
        invitados[usuario] = true;
    }

    // Función para consultar si una dirección especifica tiene invitación
    function consultarInvitados(address usuario) public view returns (bool) {
        return invitados[usuario];
    }
}
</code></pre>

En este ejemplo, cada vez que alguien llama a la función `invitar` y pasa un address como parámetro, su valor en el mapping `invitados` cambia a `true`. Puedes consultar si cualquier dirección está invitada o no usando `consultarInvitados`.

### Cosas que debes saber sobre los mappings:

1. **No puedes iterar sobre un mapping**: A diferencia de un array, no puedes recorrer todos los elementos de un mapping. Esto significa que no hay manera fácil de "listar" todas las claves almacenadas. Si necesitas hacer eso tendrás que mantener un array separado con las claves o usar algún tipo de estructura adicional.
2. **Valores por defecto**: Si intentas acceder a un valor que no existe, el mapping te devolverá el valor por defecto del tipo de dato del valor. Esto puede ser útil, pero también puede llevar a confusiones si no lo manejas correctamente.
3. **Mappings anidados**: Puedes tener mappings dentro de mappings. Por ejemplo, un mapping que asocie direcciones con otro mapping de enteros, como un súper cajón con sub-cajones dentro.
