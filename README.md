# hardhat gitpod

This project is a boilerplate for building smart contracts for EVM copatible networks using HardHat on https://Gitpod.io. You can do your entire development in the cloud environment. No need to install anything locally, just a web browser is enough. 

Compile, test and deploy a smart contract to the Polygon Mumbai test network, then interact with it. Get all of the knowledge and tools you need in order to deploy your own smart contracts to the blockchain. 

## It starts from the most basic setup possible:

1. A package.json that includes all of the necessary packages for HardHat development
2. A .gitpod.yml that runs npm install
3. This README.md file with all of the instructions you need
4. A [DEVLOG.md](DEVLOG.md) file that documents the entire development process I did in a blog format, just in case you are interested, or if you are looking for a solution to a specific problem. I hope you find it educational and useful. 

## How to develop, test and depoly your contract

At the moment of writing, the Lock.sol contract can be compiled, tested and deployed to Polygon Mumbai. 

### Install MetaMask and get some free test Matic

- Install the MetaMask extension from the Chrome webstore
- Register to https://alchemy.com
- Create a new Alchemy app on the dashboard. Enter the app details
- From the menu press 'Add to wallet'. This will add the Alchemy RPC endpoint to your Metamask for Polygon Mumbai
- From the menu press 'Get test tokens'
- Copy your wallet address and paste into the Alchemy faucet. You got test MATIC!

### Set your blockchain RPC endpoint and wallet's private key in .env

- Copy the .env-example file to .env
- From your Alchemy App's dashboard, press 'API Key' and copy the HTTPS field to .env ALCHEMY_API_URL
- Copy your Metamask account's private key to .env PRIVATE_KEY
- Save .env

Now your are ready to interact with the Polygon Mumbai blockchain. Please note that the network settings can be found in hardhat.config.js.

### Compile, test and deploy contract

The test contract is under ./contracts/Lock.sol. We are now going to test, compile and deploy it, then interact with it. 

```bash
$ npx hardhat compile
$ npx hardhat test
```

If the compilation and test go through well, deploy to Polygon Mumbai

```bash
$ npx hardhat run scripts/deploy.js --network mumbai
```

If the contract is successfully deployed, you should get a contract address

### Locate your contract on Polygonscan

Open https://mumbai.polygonscan.com/ and search for your contract address. Examine the contract creation transaction. How much did it cost to deploy the contract?

### Save your contract address in the environment variables

Copy the contract address and save it to LOCK_CONTRACT_ADDRESS in .env. 

**IMPORTANT:** Remove the 0x from the beginning of the address in the .env variable. For example, if the contract address is 0x6B9dcebAE60Dcb9709CEaAE8dbE218DfB33a5E18, the variable definition should be 

```text
LOCK_CONTRACT_ADDRESS=6B9dcebAE60Dcb9709CEaAE8dbE218DfB33a5E18
```

## Interact with your contract on the blockchain

Now that your contract is deployed and its address is defined in the environment variables, it's time to use the ./scripts/interactWithLock.js script to see if Mumbai is willing to provide services based on it. 

Take a look at the code in ./scripts/interactWithLock.js. Try to locate the variable that reads the contract address from .env. 

Now let's put it to the test:

```bash
$ npx hardhat run scripts/interactWithLock.js --network mumbai
```

Was your withdrawal successful? I hope it was. 

Open your Alchemy app dashboard and take a look at the request log at the bottom of the app dashboard. Which requests did the interaction script make to the blockchain? 

## Congrats! You have a working HardHat environment

Now is the time to start exprimenting with [OpenZeppelin](https://wizard.openzeppelin.com/)

## Clean your environment

In order to create a new contract, it is advised to start a new repo:

- Save your environment variables somewhere
- Fork this project
- Remove Lock.sol from ./contract
- remove Lock.js from ./test
- remove interactWithLock.js from ./scripts
- Set your Alchemy and private key environment variables in the new project

Anyway, whenever you would like to get rid of contract compilation artifacts in your project, run the follwind command:

```bash
$ npx hardhat clean
```

## Deploy a new contract 

- Add your new contract file to ./contracts
- Write tests for it and place them in ./test/<Contractname>.js
- Compile and test your contract

### Deploy to Polygon Mumbai

Copy ./scripts/deploy.js into a new script that is similar to the existing deploy script, but references your contract and the details relevant to it. 

Run the deployment script (assuming it is deployscript.js):

```bash
npx hardhat run scripts/deployscript.js --network mumbai
```

- Create a new variable in .env for your script address
- Create an interaction script and try to interact with your newly deployed script

Well done, you are an Ethereum contract deployer. Try to experiment with various types of contracts and interacting with them. What are their limitations? How would you modify the contract in order to provide a new type of service?

## Next up, build a front end web app for your contract

Now that you know how to deploy smart contract and interact with them, why not let others play around with their features? Learn how to create a front end web app for your smart contract and deploy it to the web (or even to IPFS), then let users log in with MetaMask and interact with your smart contract. 