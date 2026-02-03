---
icon: square-small
---

# Introducción a Criptografía

La criptografía es otro pilar fundamental en el funcionamiento de las blockchain. Sin ella sería prácticamente imposible garantizar la seguridad y la integridad de las transacciones y datos almacenados. Pero, ¿cómo funciona exactamente la criptografía en este contexto?

Todo comienza con las **funciones hash criptográficas**. Estas funciones toman una entrada de cualquier tamaño y producen una salida de tamaño fijo, conocida como hash. Lo interesante es que, si cambias aunque sea un solo carácter en la entrada, el hash resultante será completamente diferente. Esto asegura que cualquier alteración en un bloque sea fácilmente detectable, ya que el hash del bloque cambiaría y rompería la cadena.

<figure><img src="../.gitbook/assets/Hhola (1).png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/hola.png" alt="" width="563"><figcaption></figcaption></figure>

Como puedes observar, el hash cambia completamente a pesar de que solo estamos cambiando la "H" mayúscula por la minúscula. Puedes experimentar con los hash en la siguiente página:

{% embed url="https://10015.io/tools/sha256-encrypt-decrypt" %}

Además, cada bloque en la blockchain contiene el hash del bloque anterior, creando una cadena inmutable de bloques enlazados. Si alguien intentara modificar un bloque anterior, tendría que recalcular los hashes de todos los bloques siguientes, lo cual es computacionalmente inviable en una red grande y distribuida.

Otro componente esencial es el **sistema de clave pública y clave privada**. Cada usuario en la blockchain tiene un par de claves:

* Clave Pública: se puede compartir con otros, es como si fuera tu correo electrónico. Funciona como una dirección a la que otros pueden enviar transacciones Clave Privada: se debe mantener en secreto, es como si fuera tu contraseña. Es utilizada para firmar digitalmente las transacciones que envías, demostrando que eres el propietario de los fondos.

Cuando realizas una transacción esta es firmada con tu clave privada. Los nodos de la red pueden verificar esta firma utilizando tu clave pública, sin necesidad de conocer tu clave privada. Esto garantiza que las transacciones sean auténticas y que solo el dueño legítimo pueda mover los fondos asociados a esa clave pública.

La criptografía también juega un papel crucial en mantener el anonimato (o más bien el seudonimato) en las transacciones. Aunque todas las transacciones son públicas, están asociadas a direcciones que no necesariamente revelan la identidad real del usuario. Sin embargo, es importante recordar que con suficiente análisis es posible rastrear transacciones y potencialmente identificar a los usuarios.

