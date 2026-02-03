---
icon: square-small
---

# Convirtiendo una Subnet en una L1

Ahora con el Nodo RPC configurado, es momento de darle vida a nuestra blockchain L1. Pasaremos a la tercera sección del Toolbox, convertir nuestra subnet en una L1.

Lo primero que haremos es seleccionar la subnet que creamos en la primera sección, el Toolbox la reconocerá por defecto.

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

## Validator Manager

Cuando conviertes una Subnet en una L1, el conjunto de validadores que aseguran la red pasa a ser administrado por un Validator Manager Contract. Este contrato inteligente puede implementar diferentes lógicas de validación, como Proof-of-Authority (PoA), Proof-of-Stake (PoS) o un sistema personalizado.

Debes especificar el **ID de la blockchain** donde se desplegará el contrato del gestor de validadores. En este caso seleccionaré la blockchain que creamos.

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

La herramienta despliega un proxy estándar de OpenZeppelin para permitir **actualizaciones futuras** sin necesidad de volver a desplegar desde cero.

## Validadores iniciales

Antes de completar la conversión a L1, necesitas añadir **al menos un validador inicial**.

Para cada validador, debes indicar:

* **NodeID** (identificador único de tu nodo).
* **Proof of Possession (PoP)**: prueba criptográfica de que controlas la clave privada del nodo.
* **Consensus weight**: peso que tendrá en el consenso.
* **Initial balance**: fondos iniciales que se asignarán.
* **Dirección de control**: una cuenta (o multi-sig) que pueda desactivar el validador y retirar sus fondos.

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

Ejecuta el comando que te proporciona la interfaz en la consola de la instancia:

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

Copia el resultado dentro del input en el Toolbox y dale al botón "Add Validator".

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

Esta pantalla es la configuración final de un validador antes de convertir tu Subnet en L1:

* **Node ID:** este valor identifica de forma inequívoca a tu validador dentro de la red.
* **Consensus Weight:** representa el peso de voto del validador en el consenso. En este caso al solo tener un nodo, este tendrá el 100%. En producción, un solo nodo no debería superar el **20% del peso total**, para evitar centralización.
* **Validator Balance:** es la cantidad de AVAX en P-Chain que asignas para que el validador esté activo. En este caso se asignan **1 AVAX**, lo que cubriría aproximadamente 23 días, con una tarifa de 1.33 AVAX/mes. Si pones menos, el validador dejará de funcionar antes; si pones más, tendrá mayor tiempo activo.
* **Remaining Balance Owner Addresses:** es la dirección en P-Chain que recibirá el balance restante del validador cuando este deje de validar. Se usa para recuperar fondos no gastados.
* **Deactivation Owner Addresses:** es la dirección en P-Chain autorizadas para desactivar este validador antes de que expire su periodo.

Una vez configurado, dale al botón de "Convert to L1". Si todo salió bien, deberías ver este mensaje.

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>
