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

# Mapping Doble

Si un mapping ya te parece genial, espera a conocer los **mappings dobles**. Son la herramienta perfecta para situaciones donde necesitas almacenar información más compleja, como permisos de acceso, datos por categorías o cualquier cosa que necesite dos niveles de organización.

### ¿Qué es un mapping doble?

Un **mapping doble** es simplemente un mapping dentro de otro mapping. Imagina que tienes un armario (primer mapping) y, dentro de cada cajón, tienes otro armario más pequeño (segundo mapping). De esta forma, puedes almacenar datos en dos niveles de claves.

**Sintaxis básica:**

```solidity
mapping(tipoClave1 => mapping(tipoClave2 => tipoValor)) public nombreDelMapping;
```

Por ejemplo, supongamos que quieres llevar un registro de permisos por usuario y por aplicación:

```solidity
mapping(address => mapping(string => bool)) public permisos;
```

En este caso, `permisos` toma dos claves:

1. Una dirección (`address`) para identificar al usuario.
2. Un string (`string`) para identificar la aplicación.

El valor almacenado es un booleano (`bool`) que indica si ese usuario tiene permiso o no para esa aplicación específica.

### Ejemplo práctico de mapping doble

Vamos a ver un ejemplo donde almacenamos y consultamos permisos de acceso:

<pre class="language-solidity"><code class="lang-solidity">// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;
<strong>
</strong><strong>contract SistemaDePermisos {
</strong>    // Mapping doble: usuario => (aplicación => permiso)
    mapping(address => mapping(string => bool)) public permisos;

    // Función para asignar permisos a un usuario en una aplicación específica
    function asignarPermiso(address usuario, string memory aplicacion, bool tienePermiso) public {
        permisos[usuario][aplicacion] = tienePermiso;
    }

    // Función para consultar si un usuario tiene permiso en una aplicación específica
    function consultarPermiso(address usuario, string memory aplicacion) public view returns (bool) {
        return permisos[usuario][aplicacion];
    }
}
</code></pre>

En este contrato, cada usuario (`address`) tiene un mapping asociado que guarda permisos para diferentes aplicaciones (`string`). Con la función `asignarPermiso`, puedes conceder o revocar permisos, y con `consultarPermiso` puedes verificar si un usuario tiene acceso a una aplicación específica. Vamos a visualizar cómo se vería esto en una tabla:

| **Usuario (address)** | **Aplicación** | **Permiso** |
| --------------------- | -------------- | ----------- |
| 0x123...abc           | "Facebook"     | true        |
| 0x123...abc           | "Twitter"      | false       |
| 0x456...def           | "Instagram"    | true        |
| 0x789...ghi           | "Facebook"     | false       |

En esta tabla, el primer usuario (`0x123...abc`) tiene permiso para usar "Facebook" pero no para "Twitter". Mientras que el segundo usuario (`0x456...def`) tiene acceso a "Instagram" y el tercero (`0x789...ghi`) no tiene permiso para "Facebook".

### Ventajas de los mappings dobles

1. **Organización por niveles**: Perfecto para escenarios donde necesitas varios niveles de datos, como usuarios y permisos, categorías y subcategorías, etc.
2. **Acceso rápido y eficiente**: A pesar de tener dos niveles, acceder a un valor es rápido porque Solidity sabe cómo navegar estos mappings.
3. **Flexibilidad**: Puedes agregar o quitar permisos sin preocuparte por la estructura del contrato; simplemente actualizas el mapping correspondiente.
