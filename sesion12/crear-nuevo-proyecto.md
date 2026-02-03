---
icon: square-small
---

# Crear nuevo proyecto

Para crear un nuevo proyecto con Foundry debes usar la terminal. Ejecuta:

```bash
forge init MiPrimerProyecto
```

Esto creará una carpeta llamada `MiPrimerProyecto` con la estructura base del entorno de trabajo (src, test, script y el `foundry.toml`). Luego entra al proyecto:

```bash
cd MiPrimerProyecto
```

Para abrir esa carpeta en tu editor, ejecuta el comando correspondiente:

Para Visual Studio Code:

```bash
code .
```

Para Cursor:

```bash
cursor .
```

Para Antigravity:

```bash
antigravity .
```

Cuando abra tu editor de codigo, deberías ver algo como esto:\
![](<../.gitbook/assets/image (2).png>)

Vamos a ver que significa cada cosa:

* **`lib/`**: aquí se instalan las dependencias (librerías externas) que tu proyecto usa.
* **`script/`**: contiene tus scripts de automatización (`.s.sol`), típicamente para deploy, migraciones e interacciones con contratos.
* **`src/`**: aquí va el código principal, tus smart contracts (`.sol`).
* `test/`: aquí van tus tests (`.t.sol`). Es donde validas que tu código funciona y que no se rompe con cambios.
* `foundry.toml`: es el archivo de configuración de Foundry. Define parámetros como versión de Solidity, optimizer, rutas del proyecto, remappings, RPC endpoints, etc.
