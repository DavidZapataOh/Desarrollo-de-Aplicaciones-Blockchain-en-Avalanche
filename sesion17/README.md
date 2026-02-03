---
icon: browser
---

# Sesión 18: Conexión FrontEnd

Por fin llegamos a la parte donde todo lo "mágico" de la blockchain se junta con lo que ve el usuario en su pantalla.

Hasta ahora hemos creado nuestros contratos, ejecutamos comandos en la terminal y… sí, bastante teoría. Pero si nuestro usuario no puede tocar tu contrato desde un botón en la web, todo queda como en un laboratorio. Así que vamos a levantar una Dapp que:

1. Permite a las personas iniciar sesión con su wallet
2. Verifica si la persona está en una whitelist usando un Merkle Tree
3. Si pasa la prueba le deja mintear su NFT con un clic
