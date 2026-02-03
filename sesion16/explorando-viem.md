---
icon: square-small
---

# Explorando Viem

Viem es una librería superpoderosa para interactuar con blockchains compatibles con la EVM. A diferencia de ethers.js que muchos conocían antes, Viem está optimizada para TypeScript y funciona muy bien con los hooks de wagmi.

Para este ejemplo, nosotros tendremos que desplegar el siguiente contrato inteligente en la red de Avalanche Fuji, y guardar su contract address y el ABI.

```solidity
// SPDX-License-Identifier: MIT
// Compatible with OpenZeppelin Contracts ^5.0.0
pragma solidity ^0.8.24;

import {ERC721} from "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import {ERC721URIStorage} from "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";
import {Ownable} from "@openzeppelin/contracts/access/Ownable.sol";
import {MerkleProof} from "@openzeppelin/contracts/utils/cryptography/MerkleProof.sol";

contract MerkelNFT is ERC721, ERC721URIStorage, Ownable {
    uint256 private _nextTokenId;
    bytes32 public merkleRoot;
    mapping(address => bool) public hasMinted;

    constructor(address initialOwner)
        ERC721("MerkleNFT", "MKN")
        Ownable(initialOwner)
    {}

    function setMerkleRoot(bytes32 _merkleRoot) external onlyOwner {
        merkleRoot = _merkleRoot;
    }

    function whitelistMint(bytes32[] calldata _merkleProof, string memory uri) public returns (uint256) {
        bytes32 leaf = keccak256(abi.encodePacked(msg.sender));
        require(MerkleProof.verify(_merkleProof, merkleRoot, leaf), "Direccion no incluida en la whitelist");
        
        require(!hasMinted[msg.sender], "Ya has minteado tu NFT");
        hasMinted[msg.sender] = true;
        
        uint256 tokenId = _nextTokenId++;
        _safeMint(msg.sender, tokenId);
        _setTokenURI(tokenId, uri);
        return tokenId;
    }
    

    function safeMint(address to, string memory uri)
        public
        onlyOwner
        returns (uint256)
    {
        uint256 tokenId = _nextTokenId++;
        _safeMint(to, tokenId);
        _setTokenURI(tokenId, uri);
        return tokenId;
    }

    // The following functions are overrides required by Solidity.

    function tokenURI(uint256 tokenId)
        public
        view
        override(ERC721, ERC721URIStorage)
        returns (string memory)
    {
        return super.tokenURI(tokenId);
    }

    function supportsInterface(bytes4 interfaceId)
        public
        view
        override(ERC721, ERC721URIStorage)
        returns (bool)
    {
        return super.supportsInterface(interfaceId);
    }
}
```

Ahora, vamos a crear una carpeta utils dentro de la carpeta app, y ahí dentro crearemos un archivo contract.ts donde configuramos nuestra conexión con el contrato:

```typescript
import { createPublicClient, http, createWalletClient, custom } from 'viem';
import { avalancheFuji } from 'viem/chains';

// ABI del contrato (versión simplificada)
export const merkelNftAbi = [
  {
    inputs: [
      {
        internalType: 'address',
        name: 'initialOwner',
        type: 'address',
      },
    ],
    stateMutability: 'nonpayable',
    type: 'constructor',
  },
  {
    inputs: [
      {
        internalType: 'bytes32[]',
        name: '_merkleProof',
        type: 'bytes32[]',
      },
      {
        internalType: 'string',
        name: 'uri',
        type: 'string',
      },
    ],
    name: 'whitelistMint',
    outputs: [
      {
        internalType: 'uint256',
        name: '',
        type: 'uint256',
      },
    ],
    stateMutability: 'nonpayable',
    type: 'function',
  },
  {
    inputs: [
      {
        internalType: 'address',
        name: '',
        type: 'address',
      },
    ],
    name: 'hasMinted',
    outputs: [
      {
        internalType: 'bool',
        name: '',
        type: 'bool',
      },
    ],
    stateMutability: 'view',
    type: 'function',
  },
  {
    inputs: [],
    name: 'owner',
    outputs: [
      {
        internalType: 'address',
        name: '',
        type: 'address',
      },
    ],
    stateMutability: 'view',
    type: 'function',
  },
  {
    inputs: [
      {
        internalType: 'bytes32',
        name: '_merkleRoot',
        type: 'bytes32',
      },
    ],
    name: 'setMerkleRoot',
    outputs: [],
    stateMutability: 'nonpayable',
    type: 'function',
  },
  {
    inputs: [],
    name: 'merkleRoot',
    outputs: [
      {
        internalType: 'bytes32',
        name: '',
        type: 'bytes32',
      },
    ],
    stateMutability: 'view',
    type: 'function',
  },
];

// Direccion del contrato (cambiar por la tuya cuando lo despliegues)
export const contractAddress = '0x5071a042F165646Ae8522F2f8848364F4194bCD6';

// Cliente público para leer del blockchain
export const publicClient = createPublicClient({
  chain: avalancheFuji,
  transport: http('https://api.avax-test.network/ext/bc/C/rpc'),
});

// Función para crear cliente de wallet
export function getWalletClient(wallet: any) {
  return createWalletClient({
    chain: avalancheFuji,
    transport: custom(wallet),
  });
}
```
