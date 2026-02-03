---
icon: square-small
---

# Desplegando un Token en nuestra L1

Para empezar a darle vida a la L1 que acabamos de crear, lo que haremos en crear y desplegar un token ERC20 en ella.

## Creando contrato en Openzeppelin Wizard

Crearemos un token ERC20 básico con la herramienta de Openzeppelin Wizard.

{% embed url="https://wizard.openzeppelin.com/" %}

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

Una vez configurado, lo que haremos es darle al botón de "Open in Remix".

Lo primero será compilar el contrato.

<figure><img src="../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

Luego, en la sección de despliegue, seleccionaremos "Inject Provider - Core" en la opción de Enviroment. Debes estar conectado en tu extensión de Core en la red de tu L1 como lo hicimos en la sección anterior.

Verifiquemos que el ID Network coincida con el ID que le dimos a nuestra L1, en mi caso, la 44044.

<figure><img src="../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

Pasa como parametro el address de la persona que recibirá el suministro de tokens y despliega el contrato.

Para verificar que el contrato fue desplegado correctamente en nuestra L1, copia el address del contrato desplegado:

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

