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

# Otros ERC's Interesantes

A medida que el ecosistema de Ethereum ha evolucionado, se han creado muchos otros estándares ERC para ampliar las funcionalidades de los contratos inteligentes. A continuación, te presentamos algunos de los ERCs más interesantes que complementan o amplían las capacidades de los ERC20, ERC721 y ERC1155.

### **ERC777 - Tokens Avanzados con Hooks**

El **ERC777** introduce la posibilidad de ejecutar "hooks" en cada transferencia de tokens, proporcionando más flexibilidad y seguridad. Es compatible con ERC20, pero mejora su funcionalidad al permitir que los contratos reaccionen a las transferencias.

* **Características**:
  * Permite que contratos intercepten y procesen transferencias.
  * Mejora la eficiencia en transacciones complejas.
* **Aplicación**: Utilizado en aplicaciones financieras descentralizadas (DeFi) donde se necesitan acciones automatizadas, como comisiones o notificaciones.

### **ERC4626 - Vaults Estandarizados para Tokens**

El **ERC4626** es un estándar para "vaults" o bóvedas que almacenan tokens, facilitando el desarrollo de aplicaciones DeFi donde los usuarios pueden depositar tokens en un pool común.

* **Características**:
  * Proporciona una API estándar para depósitos y retiros de tokens.
  * Facilita la interoperabilidad entre protocolos DeFi que usan vaults.
* **Aplicación**: Utilizado en plataformas de staking y yield farming, permitiendo a los usuarios depositar y ganar rendimiento de manera estandarizada.

### **ERC998 - Tokens Compuestos o de Propiedad Jerárquica**

El **ERC998** permite crear tokens compuestos donde un token puede "poseer" otros tokens, lo cual es ideal para activos digitales complejos.

* **Características**:
  * Un NFT puede poseer otros NFTs o tokens ERC20.
  * Permite estructuras de propiedad jerárquica.
* **Aplicación**: Popular en juegos y mundos virtuales, donde personajes o ítems pueden contener otros objetos o recursos digitales.

### **ERC725 - Identidad Descentralizada**

El **ERC725** es un estándar para la identidad digital en Ethereum, proporcionando un sistema para perfiles de identidad que los usuarios controlan.

* **Características**:
  * Soporte para almacenamiento seguro de datos personales.
  * Facilita la creación de identidades verificables en la blockchain.
* **Aplicación**: Útil para aplicaciones de identidad digital y verificaciones KYC (Know Your Customer) descentralizadas.

### **ERC948 - Suscripciones en la Blockchain**

El **ERC948** define un sistema para pagos recurrentes y suscripciones en la blockchain, proporcionando una estructura para servicios de pago recurrente.

* **Características**:
  * Diseño para pagos automáticos y recurrentes.
  * Ideal para servicios de suscripción descentralizados.
* **Aplicación**: Perfecto para servicios de suscripción como plataformas de contenido, permitiendo pagos automáticos sin intermediarios.

### **ERC1400 - Tokens de Seguridad (Security Tokens)**

El **ERC1400** es un estándar creado específicamente para tokens de seguridad, con características avanzadas de control de accesos, cumplimiento y transparencia, que cumplen con regulaciones legales.

* **Características**:
  * Controles de acceso y restricciones de transferencias.
  * Transparencia y cumplimiento regulatorio.
  * Eventos de retención y liberación de tokens.
* **Aplicación**: Usado en ofertas de tokens de seguridad (STO) y aplicaciones financieras donde se requiere el cumplimiento de regulaciones de valores.

### **ERC6551 - Cuentas Asociadas a NFTs**

El **ERC6551** permite que cada NFT tenga una cuenta de contrato asociada, lo cual expande las posibilidades de los NFTs, permitiéndoles realizar transacciones y poseer otros activos.

* **Características**:
  * Cada NFT tiene una cuenta de contrato que actúa de forma independiente.
  * Permite a los NFTs tener otros activos en su propiedad.
* **Aplicación**: Útil en juegos y mundos virtuales donde los NFTs representan personajes o ítems que pueden interactuar con otros contratos o poseer activos propios.

### **ERC4973 - Cuentas Vinculadas**

El **ERC4973** es un estándar para crear "cuentas vinculadas" o "bound accounts", donde una cuenta está directamente asociada a un token, y no se puede transferir o separar del mismo.

* **Características**:
  * Soporte para tokens no transferibles, diseñados para identidad o membresía.
  * Crea una vinculación entre una cuenta y un token específico.
* **Aplicación**: Ideal para certificados, insignias y activos personales no transferibles, donde se necesita una asociación directa entre un usuario y el token.

### **ERC1726 - Tokens con Distribución de Dividendos**

El **ERC1726** define un estándar para tokens que distribuyen dividendos, permitiendo a los titulares recibir automáticamente ingresos generados, como dividendos o pagos por préstamos tokenizados. Este estándar facilita la visualización y administración de dividendos distribuidos, ayudando a los holders a recibir sus ganancias de forma eficiente.

* **Características**:
  * Define una interfaz estándar para consultar dividendos acumulativos y disponibles.
  * Compatible con ERC20 y otros estándares de tokens que generan ingresos pasivos.
* **Aplicación**: Es ideal para tokens que representan derechos a flujos de efectivo futuros, como dividendos o pagos de préstamos en plataformas DeFi, asegurando una distribución transparente y compatible con wallets y exchanges.
