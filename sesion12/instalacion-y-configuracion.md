---
icon: square-small
---

# Instalación y Configuración

## Requisitos previos

### Recomendado

* **Git** instalado (instálalo [aquí](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) si no lo tienes)
* **Una terminal**:
  * macOS / Linux: terminal normal
  * Windows: **WSL2** (wsl --install)
* **Un editor de código** (recomendado: [Antigravity](https://antigravity.google/) / [Cursor](https://cursor.com/))

## Instalación

En la terminal ejecuta:

```bash
curl -L https://foundry.paradigm.xyz | bash
```

Cuando finalice la instalación ejecuta:

```bash
foundryup
```

{% hint style="warning" %}
Si no detecta la instalación, cierra y vuelve a abrir la terminal, y vuelve a ejecutar el comando.
{% endhint %}

Verifica la instalación

```bash
forge --version
```

## Configurando Editor de código

Para tener una mejor visualización del código de Solidity, se recomienda instalar una extensión que lo soporte.

Para eso, entra en el editor de código en el cual vas a trabajar, y busca en el panel izquierdo la opción de "Extensions".

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

En la parte superior verás un buscador, escribe "Solidity". Te saldrán varios resultados:

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Los más usados hoy son los de **NomicFoundation** y **juanblanco,** ambos open-source. Puedes empezar con cualquiera. Antes de instalar, revisa el número de descargas, las reseñas y el historial de actualizaciones para reducir el riesgo de extensiones maliciosas.
