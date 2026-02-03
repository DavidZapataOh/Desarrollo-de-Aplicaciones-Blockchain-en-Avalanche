---
icon: square-small
---

# Llamar Contrato desde la Web

¿Recuerdas la pagina de inicio que nos muestra Next cuando lo ejecutamos? Vamos a hacer unos cambios para poder adaptarlo a las necesidades que tenemos.

Ve a page.tsx y reemplaza el codigo que hay allí por el siguiente:

```tsx
'use client';

import { useEffect, useState } from 'react';
import { usePrivy } from '@privy-io/react-auth';
import Image from 'next/image';
import { getMerkleProof, isAddressInWhitelist, getMerkleRoot } from './utils/merkleTree';
import { contractAddress, merkelNftAbi, publicClient, getWalletClient } from './utils/contract';

export default function Home() {
  const { login, logout, authenticated, user, ready } = usePrivy();
  const [hasMinted, setHasMinted] = useState<boolean>(false);
  const [loading, setLoading] = useState<boolean>(false);
  const [txHash, setTxHash] = useState<string>('');
  const [error, setError] = useState<string>('');
  const [inWhitelist, setInWhitelist] = useState<boolean>(false);
  const [isOwner, setIsOwner] = useState<boolean>(false);
  const [currentMerkleRoot, setCurrentMerkleRoot] = useState<string>('');

  // Función para verificar estado actual en la blockchain
  const checkBlockchainStatus = async () => {
    if (!authenticated || !user?.wallet?.address) return;
    
    try {
      setLoading(true);
      
      // Verificar merkle root actual
      try {
        const merkleRoot = await publicClient.readContract({
          address: contractAddress as `0x${string}`,
          abi: merkelNftAbi,
          functionName: 'merkleRoot',
        }) as `0x${string}`;
        setCurrentMerkleRoot(merkleRoot);
        console.log("Merkle Root actual:", merkleRoot);
      } catch (err) {
        console.error("Error al leer merkle root:", err);
      }
      
      // Verificar si ya ha minteado
      try {
        const data = await publicClient.readContract({
          address: contractAddress as `0x${string}`,
          abi: merkelNftAbi,
          functionName: 'hasMinted',
          args: [user.wallet.address],
        });
        setHasMinted(Boolean(data));
      } catch (err) {
        console.error('Error al verificar estado de minteo:', err);
      }
      
      // Verificar si el usuario es propietario
      try {
        const ownerAddress = await publicClient.readContract({
          address: contractAddress as `0x${string}`,
          abi: merkelNftAbi,
          functionName: 'owner',
        }) as `0x${string}`;
        setIsOwner(ownerAddress.toLowerCase() === user.wallet.address.toLowerCase());
      } catch (err) {
        console.error('Error al verificar propietario:', err);
      }
      
      // Verificar whitelist basado en merkle root actual
      const isInWhitelist = isAddressInWhitelist(user.wallet.address);
      setInWhitelist(isInWhitelist);
      
    } catch (err) {
      console.error('Error al verificar estado:', err);
    } finally {
      setLoading(false);
    }
  };

  // Verificar estado cuando cambia la autenticación o wallet
  useEffect(() => {
    if (ready) {
      checkBlockchainStatus();
    }
  }, [authenticated, ready, user?.wallet?.address]);

  const handleMint = async () => {
    if (!authenticated || !user?.wallet?.address) {
      return login();
    }

    try {
      setLoading(true);
      setError('');

      if (!inWhitelist) {
        setError('Tu dirección no está en la whitelist');
        setLoading(false);
        return;
      }

      if (hasMinted) {
        setError('Ya has minteado tu NFT');
        setLoading(false);
        return;
      }

      // Obtener merkle proof
      const proof = getMerkleProof(user.wallet.address);
      console.log("Proof para minteo:", proof);
      
      // Preparar wallet para firmar transacción
      const walletClient = getWalletClient(window.ethereum);
      
      // URI del NFT (podría ser dinámico)
      const nftURI = 'ipfs://bafkreiavma4dp5efkuiegbwlfys6jlrf6cct3e5keesnkpzpyelyyxmkpu';
      
      // Llamar al contrato
      const hash = await walletClient.writeContract({
        address: contractAddress as `0x${string}`,
        abi: merkelNftAbi,
        functionName: 'whitelistMint',
        args: [proof, nftURI],
        account: user.wallet.address as `0x${string}`,
      });

      setTxHash(hash);
      setHasMinted(true);
    } catch (err: any) {
      console.error('Error al mintear:', err);
      setError(err.message || 'Error al mintear el NFT');
    } finally {
      setLoading(false);
    }
  };

  const setMerkleRoot = async () => {
    if (!authenticated || !isOwner) {
      setError('Solo el propietario puede configurar el merkleRoot');
      return;
    }

    try {
      setLoading(true);
      setError('');
      
      // Obtener la raíz del merkle tree
      const root = getMerkleRoot();
      console.log("Configurando Merkle Root:", root);
      
      // Preparar wallet para firmar transacción
      const walletClient = getWalletClient(window.ethereum);
      
      // Llamar al contrato
      const hash = await walletClient.writeContract({
        address: contractAddress as `0x${string}`,
        abi: merkelNftAbi,
        functionName: 'setMerkleRoot',
        args: [root],
        account: user?.wallet?.address as `0x${string}`,
      });

      console.log("Transacción de configuración merkleRoot:", hash);
      alert("MerkleRoot configurado correctamente");
      
      // Actualizar estado después de cambiar merkle root
      setTimeout(checkBlockchainStatus, 5000);
    } catch (err: any) {
      console.error('Error al configurar merkleRoot:', err);
      setError(err.message || 'Error al configurar merkleRoot');
    } finally {
      setLoading(false);
    }
  };

  // Manejar cambio de wallet
  const handleDisconnect = async () => {
    await logout();
    setHasMinted(false);
    setTxHash('');
    setError('');
    setInWhitelist(false);
    setIsOwner(false);
  };

  return (
    <main className="flex min-h-screen flex-col items-center justify-between p-24">
      <div className="z-10 max-w-5xl w-full items-center justify-between font-mono text-sm">
        <h1 className="text-4xl font-bold mb-8 text-center">NFT Whitelist Mint</h1>
        
        {!authenticated ? (
          <div className="flex flex-col items-center">
            <p className="mb-4">Conecta tu wallet para verificar si estás en la whitelist</p>
            <button 
              className="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded cursor-pointer"
              onClick={login}
            >
              Conectar Wallet
            </button>
          </div>
        ) : (
          <div className="flex flex-col items-center">
            <div className="flex justify-between w-full mb-4">
              <p>Conectado como: {user?.wallet?.address}</p>
                <button 
                  className="bg-red-500 hover:bg-red-700 text-white py-1 px-2 rounded cursor-pointer text-xs"
                  onClick={handleDisconnect}
                >
                  Desconectar
                </button>
            </div>
            
            <p className="mb-4">
              Estado: {inWhitelist ? "Estás en la whitelist! 🎉" : "No estás en la whitelist 😢"}
            </p>
            
            {inWhitelist && !hasMinted && (
              <button 
                className={`bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded cursor-pointer ${loading ? 'opacity-50 cursor-not-allowed' : ''}`}
                onClick={handleMint}
                disabled={loading}
              >
                {loading ? 'Procesando...' : 'Mintear NFT'}
              </button>
            )}
            
            {isOwner && (
              <div className="mt-4 p-4 bg-gray-100 rounded w-full text-black text-center">
                <p className="text-sm font-bold mb-2">Panel de Administrador</p>
                <p className="text-xs mb-2">Merkle Root actual: {currentMerkleRoot || 'No configurado'}</p>
                <button 
                  className="bg-purple-500 hover:bg-purple-700 text-white font-bold py-2 px-4 rounded cursor-pointer mr-2"
                  onClick={setMerkleRoot}
                  disabled={loading}
                >
                  Actualizar MerkleRoot
                </button>
              </div>
            )}
            
            {hasMinted && (
              <div className="mt-4 p-4 bg-green-100 rounded">
                <p className="text-green-800">¡Felicidades! Has minteado tu NFT</p>
                {txHash && (
                  <a 
                    href={`https://testnet.snowtrace.io/tx/${txHash}`}
                    target="_blank"
                    rel="noopener noreferrer"
                    className="text-blue-500 hover:underline"
                  >
                    Ver transacción en Snowtrace
                  </a>
                )}
              </div>
            )}
            
            {error && (
              <div className="mt-4 p-4 bg-red-100 rounded">
                <p className="text-red-800">{error}</p>
              </div>
            )}
          </div>
        )}
      </div>
    </main>
  );
}
```

Un poco largo este codigo, ¿no? Vamos a desglosarlo para entender que está pasando.

## Los Estados del Componente

Primero, entendamos los estados que maneja nuestra UI:

```tsx
// Estados relacionados con el usuario
const { login, logout, authenticated, user, ready } = usePrivy();
const [isOwner, setIsOwner] = useState<boolean>(false);
const [inWhitelist, setInWhitelist] = useState<boolean>(false);

// Estados relacionados con el minteo
const [hasMinted, setHasMinted] = useState<boolean>(false);
const [loading, setLoading] = useState<boolean>(false);
const [txHash, setTxHash] = useState<string>('');
const [error, setError] = useState<string>('');

// Estado del contrato
const [currentMerkleRoot, setCurrentMerkleRoot] = useState<string>('');
```

Estos estados controlan:\
👤 Quién eres (wallet, autenticado, owner, whitelist)\
🏭 Estado del minteo (ya minteaste, cargando, hash resultante)\
⚙️ Estado del contrato (la raíz actual del merkle)

## Lectura del Contrato (el `publicClient`)

Lo primero y más sencillo es leer el estado del contrato, sin necesitar firmar nada. Para esto usamos el `publicClient`, un cliente de solo-lectura que definimos en utils/contract.ts. Veamos la función `checkBlockchainStatus` que centraliza todas las lecturas:

```tsx
const checkBlockchainStatus = async () => {
  if (!authenticated || !user?.wallet?.address) return;
  
  try {
    setLoading(true);
    
    // 1️⃣ Leemos la raíz Merkle del contrato
    try {
      const merkleRoot = await publicClient.readContract({
        address: contractAddress as `0x${string}`,
        abi: merkelNftAbi,
        functionName: 'merkleRoot',
      }) as `0x${string}`;
      setCurrentMerkleRoot(merkleRoot);
      console.log("Merkle Root actual:", merkleRoot);
    } catch (err) {
      console.error("Error al leer merkle root:", err);
    }
    
    // 2️⃣ Verificamos si ya ha minteado
    try {
      const data = await publicClient.readContract({
        address: contractAddress as `0x${string}`,
        abi: merkelNftAbi,
        functionName: 'hasMinted',
        args: [user.wallet.address],
      });
      setHasMinted(Boolean(data));
    } catch (err) {
      console.error('Error al verificar estado de minteo:', err);
    }
    
    // 3️⃣ Verificamos si es el propietario del contrato
    try {
      const ownerAddress = await publicClient.readContract({
        address: contractAddress as `0x${string}`,
        abi: merkelNftAbi,
        functionName: 'owner',
      }) as `0x${string}`;
      setIsOwner(ownerAddress.toLowerCase() === user.wallet.address.toLowerCase());
    } catch (err) {
      console.error('Error al verificar propietario:', err);
    }
    
    // 4️⃣ Verificamos whitelist localmente (basado en el merkleTree.ts)
    const isInWhitelist = isAddressInWhitelist(user.wallet.address);
    setInWhitelist(isInWhitelist);
    
  } catch (err) {
    console.error('Error al verificar estado:', err);
  } finally {
    setLoading(false);
  }
};
```

* Por qué envolver cada llamada en `try-catch` separados?\
  Si una falla, las otras siguen intentándolo. Mejor experiencia de usuario.
* Nota sobre la tipificación:\
  El `as 0x${string}` es un cast de TypeScript para asegurar que estamos pasando una dirección Ethereum válida. Viem es exigente y con razón: mejor un error en desarrollo que en producción.

## Actualizando el Estado (useEffect)

¿Pero cuándo ejecutamos toda esta verificación? Lo hacemos al cargar la página y cada vez que cambian ciertas dependencias:

```tsx
// Verificar estado cuando cambia la autenticación o wallet
useEffect(() => {
  if (ready) {
    checkBlockchainStatus();
  }
}, [authenticated, ready, user?.wallet?.address]);
```

Este hook se dispara:\
• Cuando el usuario se conecta/desconecta\
• Cuando cambia de dirección en su wallet\
• Cuando Privy termina de cargar

## Mint: La Operación de Escritura

Ahora la función que todos esperaban, el minteo del NFT. Aquí no leemos, ¡escribimos! Necesitamos:

1. Un proof válido
2. Un cliente que pueda firmar (walletClient)
3. Un URI para el metadata
4. Manejar tanto el éxito como los errores

```tsx
const handleMint = async () => {
  // Si no hay wallet, pedimos login primero
  if (!authenticated || !user?.wallet?.address) {
    return login();
  }

  try {
    setLoading(true);
    setError('');

    // 1️⃣ Verificaciones previas
    if (!inWhitelist) {
      setError('Tu dirección no está en la whitelist');
      setLoading(false);
      return;
    }

    if (hasMinted) {
      setError('Ya has minteado tu NFT');
      setLoading(false);
      return;
    }

    // 2️⃣ Generar la prueba merkle (desde nuestro utils/merkleTree.ts)
    const proof = getMerkleProof(user.wallet.address);
    console.log("Proof para minteo:", proof);
    
    // 3️⃣ Preparar wallet para firmar (acceder a window.ethereum)
    const walletClient = getWalletClient(window.ethereum);
    
    // 4️⃣ Definir la URI del NFT (metadata en IPFS)
    const nftURI = 'ipfs://bafkreiavma4dp5efkuiegbwlfys6jlrf6cct3e5keesnkpzpyelyyxmkpu';
    
    // 5️⃣ La magia: firmar y enviar la transacción
    const hash = await walletClient.writeContract({
      address: contractAddress as `0x${string}`,
      abi: merkelNftAbi,
      functionName: 'whitelistMint',
      args: [proof, nftURI],
      account: user.wallet.address as `0x${string}`,
    });

    // 6️⃣ Actualizamos UI con éxito
    setTxHash(hash);
    setHasMinted(true);
  } catch (err: any) {
    console.error('Error al mintear:', err);
    setError(err.message || 'Error al mintear el NFT');
  } finally {
    setLoading(false);
  }
};
```

**Explicando cada paso:**\
Paso 1: Validamos por duplicado en el frontend\
Paso 2: Generamos la prueba con nuestro helper merkleTree.ts\
Paso 3: Obtenemos acceso a una wallet de firma mediante getWalletClient\
Paso 4: La URI es el metadata del NFT (típicamente un JSON con nombre, imagen, etc.)\
Paso 5: Con writeContract enviamos datos a la blockchain, firmando con nuestra wallet\
Paso 6: Actualizamos la UI según el resultado

## Funciones Admin (Exclusivas del Owner)

Ahora veamos algo que solo el owner del contrato puede hacer, actualizar la raíz Merkle. Esta es una operación privilegiada típica en contratos:

```tsx
const setMerkleRoot = async () => {
  if (!authenticated || !isOwner) {
    setError('Solo el propietario puede configurar el merkleRoot');
    return;
  }

  try {
    setLoading(true);
    setError('');
    
    // 1️⃣ Obtener la raíz calculada localmente (debe coincidir con tus addresses de whitelist)
    const root = getMerkleRoot();
    console.log("Configurando Merkle Root:", root);
    
    // 2️⃣ Preparar wallet para firmar
    const walletClient = getWalletClient(window.ethereum);
    
    // 3️⃣ Llamar a la función de admin setMerkleRoot
    const hash = await walletClient.writeContract({
      address: contractAddress as `0x${string}`,
      abi: merkelNftAbi,
      functionName: 'setMerkleRoot',
      args: [root],
      account: user?.wallet?.address as `0x${string}`,
    });

    console.log("Transacción de configuración merkleRoot:", hash);
    alert("MerkleRoot configurado correctamente");
    
    // 4️⃣ Refrescar estado después de un tiempo (5s) para que la blockchain se actualice
    setTimeout(checkBlockchainStatus, 5000);
  } catch (err: any) {
    console.error('Error al configurar merkleRoot:', err);
    setError(err.message || 'Error al configurar merkleRoot');
  } finally {
    setLoading(false);
  }
};
```

## La UI Completa

Finalmente tenemos un JSX condicional con varios estados:

* No conectado -> Mostrar botón de login
* Conectado pero no en whitelist -> Mostrar mensaje de rechazo
* En whitelist y no ha minteado -> Mostrar botón de mint
* Owner -> Mostrar panel admin
* Minteado exitoso -> Mostrar congrats y link a Snowtrace



Recuerda: la comunicación con contratos inteligentes SIEMPRE sigue el mismo patrón:

1. Leer (gratis, sin firma, usuario pasivo)
2. Preparar (validar, calcular)
3. Escribir (requiere firma, gas, el usuario debe aceptar)

Si entiendes bien este flujo, construir cualquier dApp, sea un marketplace, un DAO o un juego, seguirá los mismos principios básicos.

Domina esta lógica y dominarás el desarrollo frontend de Web3!!!
