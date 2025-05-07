# soroban-hello-world-frontend

Read the docs: https://developers.stellar.org/docs/build/smart-contracts/getting-started/hello-world-frontend

This is the creation of a webapp that interacts with the Hello World contract through TypeScript bindings.

# Steps

## Create an astro project:

npm create astro@latest

## Assuming you have already deployed the contract from the soroban-hello-world-smartcontract with aliases, resuse the generated contract ID files by copying them from the soroban-hello-world/.stellar directory into this project:

Assumes you named the project stellar like I did
cp -R ../.stellar/ .stellar

## Generate an NPM package for the Hello World contract

stellar contract bindings typescript \
 --network testnet \
 --contract-id hello_world \
 --output-dir packages/hello_world

cd packages/hello_world
npm install
npm run build
cd ../..

## Call the contract from the frontend

---

import \* as Client from './packages/hello_world';

const contract = new Client.Client({
...Client.networks.testnet,
rpcUrl: 'https://soroban-testnet.stellar.org:443'
});

const { result } = await contract.hello({to: "Devs!"});
const greeting = result.join(" ");

---

<h1>{greeting}</h1>

npm run dev

# Assignment: Do the same for the increment smart contract
