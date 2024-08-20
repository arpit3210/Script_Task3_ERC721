
---

**Video Script: "How to Mint an ERC-721 Token Using Hardhat and OpenZeppelin Contracts Wizard"**

---

### **[Intro Scene]**
- **Visual**: Animated intro with the title "Minting an ERC-721 Token" with blockchain-related graphics.
- **Voiceover**: 
  "Welcome to this step-by-step guide on how to mint your very own ERC-721 token using Hardhat and the OpenZeppelin Contracts Wizard. In this video, we’ll cover the entire process, including:

1. Setting up your project in Hardhat.
2. Configuring the Swisstronik network and setting your private key.
3. Creating an ERC-721 smart contract using OpenZeppelin Contracts Wizard.
4. Deploying the contract to the Swisstronik network.
5. Minting your first ERC-721 token.
6. Publishing your code to a GitHub repository.
7. Finally, filling in the necessary details on the Swisstronik task page to complete your assignment.

By the end of this video, you'll have successfully completed the task and be ready for review by our team. Let's get started!"

---

### **[Part 1: Setting Up the Project]**
- **Visual**: Screen recording showing a terminal window and a code editor (like VS Code).
- **Voiceover**:
  "First, let’s set up our project. Open your terminal and create a new project directory by typing:"
- **Text on screen**: 
  ```
  mkdir MyERC721Token
  cd MyERC721Token
  ```
- **Voiceover**:
  "Now,  Install Hardhat if you have installed hardhat already in previous task, you don't need to install again, you just have to initalite hardhat project by simple command 
  ```
  npx hardhat
  ```

Copy this command 
```
npm install --save-dev hardhat
```

It will take few seconds to install, after installing Hardhat 

we have to initialize a new Hardhat project with the command:"
- **Text on screen**: 
  ```
  npx hardhat
  ```
- **Visual**: The terminal showing the project initialization process.
- **Voiceover**:
  "Hardhat is a development environment for Ethereum that helps you compile and deploy smart contracts. When you run `npx hardhat`, it sets up a basic project structure with all the necessary configuration files. Follow the prompts to create a JavaScript project."

---

### **[Part 2: Setting the Private Key and Configuring Swisstronik Network]**
- **Visual**: Terminal and code editor.
- **Voiceover**:
  "Before we proceed, we need to set a variable with your private key. This key is essential for signing transactions on the blockchain. Let's open our metamask wallte to get our private keys, Just open and Click on Top Right Corner on three dots and then Click on Account Details, then click in Show private keys, just copy you private keys,

 To set the variable, use the following command:  "
- **Text on screen**:
  ```
  npx hardhat vars set PRIVATE_KEY
  ```
- **Voiceover**:
  "After running the command, you will be prompted to enter your private key, you just have to paste you copied private keys here. and just hit enter"

- **Visual**: Code editor with Hardhat configuration.
- **Voiceover**:
  "Next, we need to configure the Swisstronik network in our Hardhat configuration file. Here’s the code you’ll need to add to `hardhat.config.js`:"
- **Text on screen**:
  ```javascript
  require("@nomicfoundation/hardhat-toolbox");
  
  const PRIVATE_KEY = vars.get("PRIVATE_KEY");

  module.exports = {
    defaultNetwork: "swisstronik",
    solidity: "0.8.19",
    networks: {
      swisstronik: {
        url: "https://json-rpc.testnet.swisstronik.com/",
        accounts: [`0x${PRIVATE_KEY}`],
      },
    },
  };
  ```
- **Voiceover**:
  "In this configuration, we import the necessary Hardhat tools and set the Swisstronik network URL. The `accounts` field uses the private key you stored earlier to sign transactions. This setup allows us to deploy contracts to the Swisstronik testnet."

---

### **[Part 3: Creating the ERC-721 Smart Contract]**
- **Visual**: Screen recording showing the use of the OpenZeppelin Contracts Wizard in a web browser.
- **Voiceover**:
  "Next, we need to create the ERC-721 smart contract. For this, we'll use the OpenZeppelin Contracts Wizard. Navigate to the OpenZeppelin Contracts Wizard website."
- **Visual**: The user selects ERC-721 from the options, configures the token name and symbol.
- **Voiceover**:
  "ERC-721 is a standard for creating non-fungible tokens (NFTs) on the Ethereum blockchain. The OpenZeppelin Contracts Wizard simplifies this process by allowing you to customize your token's features without writing the code from scratch. In the wizard, choose ERC-721. Set your token's name and symbol. You can also add optional features like Mintable, Burnable, or Enumerable depending on your needs."
- **Visual**: The wizard generates the code.
- **Voiceover**:
  "The wizard will generate the Solidity code for your ERC-721 token based on your configuration. Copy this code, as we'll use it in our Hardhat project."

---

### **[Part 4: Deploying the ERC-721 Smart Contract]**
- **Visual**: Switch back to the code editor.
- **Voiceover**:
  "Now, let's deploy the smart contract using Hardhat. In your project directory, create a new file in the `contracts` folder and paste the code you copied from the OpenZeppelin Contracts Wizard."
- **Visual**: The user creates and names the file `MyERC721Token.sol` and pastes the code.
- **Voiceover**:
  "Name the file `MyERC721Token.sol`. This file contains the Solidity code for your ERC-721 token. Solidity is the programming language used to write smart contracts on Ethereum."

- **Visual**: The user creates the deployment script.
- **Voiceover**:
  "Next, we need to write a deployment script. Deployment scripts are used to compile and deploy your smart contracts to the blockchain. Let’s create a new file in the `scripts` folder and call it `deploy.js`."

- **Text on screen**:
  ```
  touch scripts/deploy.js
  ```
- **Visual**: The user writes the deployment script in the `deploy.js` file.
- **Voiceover**:
  "Here’s a basic deployment script:"
- **Text on screen**:
  ```javascript
  const { ethers } = require("hardhat");

  async function main() {
    const MyERC721Token = await ethers.getContractFactory("MyERC721Token");
    const token = await MyERC721Token.deploy();
    await token.deployed();
    console.log("MyERC721Token deployed to:", token.address);
  }

  main().catch((error) => {
    console.error(error);
    process.exitCode = 1;
  });
  ```
- **Voiceover**:
  "Let me explain what’s happening here. First, we import the `ethers` library from Hardhat. This library helps us interact with the Ethereum blockchain. We then define an asynchronous `main` function where we get a contract factory for our `MyERC721Token` contract. The `deploy` method deploys the contract to the blockchain, and we wait until the contract is fully deployed using `await token.deployed()`. Finally, we log the contract’s address to the console. This address is crucial because it identifies your deployed contract on the blockchain."

- **Visual**: The terminal and editor.
- **Voiceover**:
  "To deploy your contract, run the following command in your terminal:"
- **Text on screen**:
  ```
  npx hardhat run scripts/deploy.js --network swisstronik
  ```
- **Voiceover**:
  "We’re deploying to the Swisstronik network, which we configured earlier. If the deployment is successful, you’ll see your contract's address in the terminal output."

---

### **[Part 5: Minting the ERC-721 Token]**
- **Visual**: The terminal and code editor with a focus on interacting with the deployed contract.
- **Voiceover**:
  "With our contract deployed, it's time to mint our first ERC-721 token. To do this, we'll create another script that interacts with our deployed contract."
- **Text on screen**:
  ```
  touch scripts/mint.js
  ```
- **Visual**: The user writes the minting script in the `mint.js` file.
- **Voiceover**:
  "Here’s the minting script:"
- **Text on screen**:
  ```javascript
  const { ethers } = require("hardhat");

  async function main() {
    const [deployer] = await ethers.getSigners();
    const MyERC721Token = await ethers.getContractFactory("MyERC721Token");
    const token = await MyERC721Token.attach("<deployed_contract_address>");
    
    const mintTx = await token.mint(deployer.address, 1);
    await mintTx.wait();
    
    console.log("Token minted successfully.");
  }

  main().catch((error) => {
    console.error(error);
    process.exitCode = 1;
  });
  ```
- **Voiceover**:
  "Let’s break this down. First, we get the address of the account deploying the token with `await ethers.getSigners()`. Then, we get a reference to our deployed contract using `MyERC721Token.attach("<deployed_contract_address>")`, where `<deployed_contract_address>` is the address you got when you deployed the contract."

- **Visual**: Highlight the minting function.
- **Voiceover**:
  "The key part of this script is the `mint` function, where we mint a new token by calling the `mint` function on our deployed contract. The `mint` function takes two arguments: the recipient's address (in this case, the deployer's address) and the token ID (we're using `1` here). After the minting transaction is submitted, we wait for it to be confirmed using `await mintTx.wait()`. Once confirmed, a message is logged to indicate that the token was minted successfully."

- **Visual**: The terminal with the command to run the minting script.
- **Voiceover**:
  "To mint your ERC-721 token, run the following command in your terminal:"
- **Text on screen**:
  ```
  npx hardhat run scripts/mint.js --network swisstronik
  ```
- **Voiceover**:
  "After running this command, you'll have successfully minted your first ERC-721 token on the Swisstronik network."

---

### **[Part 6: Publishing the Code to GitHub]**
- **Visual**: GitHub website and the process of creating a new repository.
- **Voiceover**:
  "With your project complete, it's time to publish the code to a GitHub repository. This step is essential for sharing your work and ensuring version control. Start by navigating to GitHub and creating a new repository."
- **Visual**: The process of pushing code to the repository using the terminal.
- **Voiceover**:
  "Once your repository is created, you can push your project files to GitHub. Use the following commands in your terminal to initialize Git, add your files, commit them, and push to the remote repository:"
- **Text on screen**:
  ```
  git init
  git add .
  git commit -m "Initial commit"
  git branch -M main
  git remote add origin <your_repository_url>
  git push -u origin main
  ```
- **Voiceover**:
  "Replace `<your_repository_url>` with the URL of your GitHub repository. This will push all your project files to GitHub, making them accessible online."

---

### **[Part 7: Filling in the Swisstronik Task Page]**
- **Visual**: Swisstronik task page and the fields that need to be filled out.
- **Voiceover**:
  "Finally, we need to fill in the required details on the Swisstronik task page to complete the assignment. Make sure to provide the GitHub repository link, the deployed contract address, and any other requested information. Once all the details are filled in, submit your task for review."
- **Visual**: Submission process on the Swisstronik task page.
- **Voiceover**:
  "Double-check all the information before submitting. A correct and complete submission will ensure your task is reviewed without any issues."

---

### **[Outro Scene]**
- **Visual**: Animated outro with links to other videos, the GitHub repository, and social media handles.
- **Voiceover**:
  "Congratulations! You've successfully minted an ERC-721 token on the Swisstronik network.  Thanks for watching, and happy coding!"

---

This script now includes detailed explanations and instructions for setting up the private key variable, configuring the Swisstronik network, and minting an ERC-721 token.
