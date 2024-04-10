# Solana NFT and Token Creation Guide

This guide provides step-by-step instructions for creating Solana NFTs and tokens using Metaplex's Candy Machine, and SPL tokens.

## Prerequisites
- **[NodeJs:](https://nodejs.org/)** Version 16 or higher
- **[Install Solana CLI:](https://docs.solana.com/cli/install-solana-cli)** If you haven't already, follow the Solana CLI Installation Guide to install the Solana Command Line Interface (CLI).
- **[Set up Phantom wallet:](https://phantom.app/)** Download and create a new wallet or use an existing one. You'll need this wallet to interact with Solana and perform the tasks below.
- **[Sugar CLI:](https://github.com/metaplex-foundation/sugar/releases/tag/v1.2.2)** Legacy Version, V1.x

## Generate a Solana Keypair
- Open your terminal.
- Run the following command to generate a new Solana keypair:
   ```
   mkdir spl-token-nft-mint
   cd spl-token-nft-mint
   solana-keygen new --outfile wallet.json
   ```
- This will create a new keypair and store it in a **wallet.json** file.
- Also airdrop 1 SOL to the account:
    ```
    solana airdrop 1 <wallet-public-key> --url https://api.devnet.solana.com
    ```
- Import the wallet's private key to Phantom wallet.

## Create and Mint a New SPL Token (MetaToken)
### Open the mint-spl-tokens folder:
   
   cd mint-spl-tokens
   
### Install dependencies: 
    
    yarn
    `or`
    npm install
    
### Add your Solana Devnet QuickNode RPC Endpoint:
    
    const umi = createUmi('REPLACE_WITH_SOLANA_RPC');
    
### (Optional) Add the IPFS URL of your token's image metadata:
    
    const metadata = {
        name: "MetaToken",
        symbol: "MTK",
        uri: "IPFS_URL_OF_METADATA",
    };

### Run the mint script:
    
    ts-node mint.ts

Upon successful execution you should see an output like this: \
`Successfully minted 1 million tokens ( 3G2wpf585WGES9mkuQuonoP2wr4RHFboAzxA5AfMf51f )`
    
## Create, Deploy, and Mint your NFT with sugar CLI
### Navigate to the `spl-token-nft-mint` directory:

    cd ../

### Confirm your sugar CLI version:

   ```
   sugar --version
   `or`
   ./sugar --version
   ```
Ensure your sugar version is the legacy version 1.x or reinstall.

### Validate, Upload, Deploy, and Verify your NFT assets
    
    sugar launch

`sugar launch` starts a chain of commands:
- `sugar validate`
- `sugar upload`
- `sugar deploy`
- `sugar verify`

Copy your **Candy machine ID** after `sugar deploy`\
A **config.json** file is generated after `sugar launch` is done running. This file contains the details of how the NFTs are to be minted.

## Use the Created SPL Token to Pay for the Mint
To use our SPL tokens to mint, we specify the SPL token address in the **config.json** file, then run `sugar deploy` to modify the NFT.

## Connect the NFT Contract to Metaplex's Candy Machine UI
### Navigate to the `candy-machine-ui` directory
    
    cd ../
    git clone https://github.com/metaplex-foundation/candy-machine-ui
    cd candy-machine-ui


### Rename `.env.example` to `.env` and fill in the necessary details

    REACT_APP_CANDY_MACHINE_ID=<YOUR_CANDY_MACHINE_ID>
    REACT_APP_SOLANA_NETWORK=devnet
    REACT_APP_SOLANA_RPC_HOST=<YOUR_SOLANA_RPC_ENDPOINT>
    SKIP_PREFLIGHT_CHECK=false

### Install dependencies
    yarn
    `or`
    npm install

### Strat the minting app
    yarn start

**PS:** If you get an error running `yarn start`, open the **package.json** file and set `"start": "SET NODE_OPTIONS=--openssl-legacy-provider && craco start"`

Thanks

---
 🚀🌟