---
icon: square-small
---

# Configurando un Nodo con Docker y AWS

En Avalanche puedes correr dos perfiles de nodo para tu L1:

* Nodo Validador: participa en el consenso. No expone RPC público.
* Nodo RPC Publico: expone un endpoint HTTPS para que wallets/dApps consulten tu cadena. No necesita hacer staking.

Los validadores aseguran la red, los RPC sirven de tráfico.

## 1. Configuración

Acá tienes dos opciones, configurarlo de manera local o mediante un servidor. En este caso, lo haremos usando un servidor de AWS usando EC2.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Crea una cuenta de AWS si aún no la tienes.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Elige el plan gratuito, nos será suficiente para hacer algunas pruebas.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Una vez creada la cuenta, ve a la consola de administración de AWS.

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

En el buscador de la consola ingresa "EC2".

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

En el panel de EC2 busca la opción de "Lanzar la Instancia".

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Ponle un nombre a la instancia y selecciona lo opción "Amazon Linux".

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

Baja un poco y cambia el tipo de instancia a una con mayor capacidad, por ejemplo, `c7i-flex.large`.

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

Ve a la sección de "Configuraciones de Red", acá nos aseguraremos de tener soporte para todos los puertos necesario. Da clic en el botón "Editar" en la esquina superior derecha.

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

En la parte inferior de esta sección, lo que haremos es agregar estas tres reglas de grupos de seguridad de entrada.

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

Una vez creado, ve al panel derecho y da clic al botón de "Lanzar Instancia". Te llevará a esta sección, da click en el botón inferior derecho de "Ver todas las instancias"

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

Ahora da clic en el ID de la instancia que acabas de crear.

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

Y dale en el botón "Conectar".

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Asegúrate de que esté seleccionada la opción de "Conéctese a través de una red pública" y dale a "Conectar".

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

Se nos abrirá esta consola donde ejecutaremos todos los comandos que nos genere el L1 Toolbox.

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

## 2. Instalar Docker

Asegúrate de seleccionar la opción de "Amazon Linux 2023+" y copia el código y ejecútalo en la terminal de tu instancia.

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

## 3. Selecciona la L1

Selecciona la Subnet ID de la L1 en la que quieres correr el nodo que creamos previamente en la sección anterior.

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

Verás que abajo aparecerá un desplegable con el nombre de la blockchain y toda su información.

## 4. Configurar tipo de nodo

En este caso seleccionaremos el "Public RPC Node", ya que nos ayudará a tener un RPC publico al cual conectarnos externamente y también lo podremos poner a validar. En un ambiente de producción lo ideal sería separar roles, tener un conjunto de nodos validadores (sin RPC publico) y otro conjunto de nodos RPC públicos (no validadores), esto evitará que los endpoints sean explotados y una sobrecarga de trafico.

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

## 5. Corre un Nodo AvalancheGo

Arranca el software central de Avalanche (`avalanchego`) dentro de un contenedor Docker, con todos los parámetros necesarios para que el nodo se conecte a la red.

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

Copia el código, que ya viene parametrizado con las configuraciones definidas previamente, y ejecutalo en la consola de tu instancia.

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

## 6. Configurar Reverse Proxy

Configura un servidor intermedio que se coloca **entre** tu nodo y los clientes que quieren acceder a él, esto lo hace accesible fuera de tu red.

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

Ejecuta el comando curl en la consola de tu instancia y pega el resultado en el input de abajo. Esa es la IP publica del servidor, necesaria para el siguiente paso, que generará el siguiente codigo que también debes ejecutar en la consola de tu instancia.

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Para ver si todo está funcionando correctamente, puedes ejecutar el siguiente comando en tu terminal local (Ojo, no el de la instancia, en tu terminal o cmd de manera local).

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Te debe dar una respuesta como esta. Para comprobar finalmente, dale clic al botón de "Check Node Health".

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

## 7. Añadir red a tu wallet

Da clic en el botón "Add to Wallet" para añadir la blocckhain que creaste a tu wallet.

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

Reconocerá los datos automaticamente, solo deberás ajustar el "Coin Name" con el nombre que quieres que tenga el token nativo de tu L1.

Abre tu wallet de Core y verás que estás conectado a la red que acabas de crear:

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>
