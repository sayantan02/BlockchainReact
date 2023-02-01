# **CodeLek Technology** - We create your Dream Projects.
![](https://www.codelek.com/static/img/favicon/apple-touch-icon.png)
Powered By: [**CodeLek Technology**](https://www.codelek.com)
# Blockchain Development using React
## _All procedures are mentioned to develop Blockchain_

Let's get started to install the prerequisites and and necessary commands for blockchain(Solidity) and React application.

## Setup
- First create a folder and name it yourself.
- Then open Visual Studio Code on that folder.
- Then create a folder named "client".
- At last create another folder named "smart_contracts" in your root folder.

## Installation & Setup
**If you have node installed in your system then good to go, or you can install Node.js from the link [here](https://nodejs.org/en/download/).**

Go to the client folder
```sh
    cd client
```
Now let's install Vite to use react easily.

```sh
npm init vite@latest
```
After executing the above command system will ask for project name, simply place **./ to use the current name**. If system asks for package name then simply place then name you want to give to the project. Then **select framework React** using the arrow keys. Then run the below command.

```sh
npm install
```
or
```sh
npm i
```
- Wait some time to complete the process.

Then you will want to start the React App
```sh
npm run dev
```
We'll download Tailwind CSS to create our app. Run the command to install and initialize:
```sh
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```
Now paste the below code to client/tailwind.config.cjs file:

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```
And paste the below code to index.css
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```
For more information visit tailwind css website: https://tailwindcss.com/docs/guides/vite

Now paste below code to App.jsx file
```html
<h1 className="text-3xl font-bold underline">
      Hello world!
</h1>
```
Change all the functions of .JSX files to arrow functions for modernization:
**from:**
```js
function App(){
    return (
    ...
    )}
}
```
**To:**
```js
const App = () =>{
    return (
    ...
    )
}
```
Now open the browser and if you see Hello World! like <ins>**Hello World!**</ins>. Underlined and Bold then the Tailwind css is installed successfully.

Now stop the server and go to smart_contracts/ folder on the terminal using commands:

```sh
ctrl ^c # To stop the server
cd ..
cd smart_contracts/
```
Now initialise this directory using command:
```sh
npm init -y
```

# Install Dependencies for SmartContracts

```sh
npm install --save-dev hardhat @nomiclabs/hardhat-waffle 'ethereum-waffle@^3.0.0' chai @nomiclabs/hardhat-ethers 'ethers@^5.0.0'
```
After successful installation (There can be some warnings and issues, ignore that for now) now run this command:

```sh
npx hardhat
```
This command will ask for some options:
- Create a Basic Javascript Project
- Press enter when it asks for root directory.
- Then type **y** to add .gitignore file.

Now you can run a command to test if hardhat is successfully installed or not. To check that type the below command:

```sh
# This will run the file under test folder in my case Lock.js
npx hardhat test 
```
If you are in VS Code make sure you installed the Solidity extension for better experience other wise you can face problems and cannot use emmet.

Now go and make **.sol** files under the contracts folder and you are good to go for coding.

### Deploy The Solidity code

To deploy you need to change some codes. Go to scripts folder in smart_contracts/ folder and there you will find a .js file and name that to **deploy.js**

```js
const hre = require('hardhat');
const main = async () => {

// Here you will have to name the entering file of smart contracts

// e.g. My Solidity file name is Transactions.sol and in that file my contract name is also Transactions so I am mentioning Transactions in getContractFactory("Transactions")

// WARNING: File name and contract name should be same.

  const Transactions = await hre.ethers.getContractFactory("Transactions");
  const transactions = await Transactions.deploy();

  await transactions.deployed();

  console.log(`Smart Contracts Deployed to: ${transactions.address}`
  );
}

const runMain = async () => {
  try {
    await main();
    process.exit(0);
  } catch (error) {
    console.error(error);
    process.exit(1);
  }
}

runMain();
```
Now we aren't ready to deploy our smart contracts to test server, yet!
First you have to install metamask to pay GAS fees to deploy to our test network.

- Install MetaMask from [here](https://metamask.io/download/)

Metamask is an extension. It is supported for almost all browsers. Go, install and create an account. you will find many tutorials how to create account in metamask, it is super easy.

After creating account you have to enable testnets to do that. Click on Ethereum Mainnet and there at the top you will find button to show testnets now click on that and enable test nets from the settings.

After enabling you will find many testnets, we will use Goerli Testnet to deploy the smart_contracts.

Now you need to add some Test Eths to the Goerli account for that we use Faucet. Go to google and search for Goerli faucet or go to this [link](https://goerlifaucet.com/). now create login and after that copy your account id from metamask. And then paste to the Goerli faucet and get some eths, it will take little time, so let them add some eths. 

After you get Eths now you need to create an account to host your application. 

- Go to [Alchemy](https://www.alchemy.com/) and signup.
- After signing up go to the dashboard. If you stuck anywhere go and see some tutorials there are lot resources out there.
- Now on the Dashboard click on create app. And then name the app as your own and Select **Ethereum** and then **Goerli**. Simply create the App.
- When your app is created now click on **view details**.
- There you will find a button called **View key**.
- Copy the Https Key.

Now go to **hardhat.config.js** file and Paste the HTTPS address anywhere as a comment.
change the whole code as below:

```js
require('@nomiclabs/hardhat-waffle');
/** @type import('hardhat/config').HardhatUserConfig */
module.exports = {
  solidity: "0.8.17",
  networks: {
    goerli: {
      url: "...", // Paste the HTTPS url here
      accounts : ['0063f8a...fa1b5265ee2'] // This is the account Private Key, Details Described Below
    },
  },
};
```

### Accounts Private Key:
- Now go to your Metamask and click on three dots and then select account details, there you will see export Private Key click on that, then you will be asked to enter your password that you created while creating Metamask Account. 
- Now when you got the Private Key, copy that and paste on the accounts list section mentioned above.

Now you are ready to deploy your smart contracts to the **Goerli TestNet**.

Open Terminal and Execute the below command:

```sh
npx hardhat run scripts/deploy.js --network goerli
```
It will take some time(Based on your PC Specifications) to Deploy code to the blockchain so please wait until it finishes.

After it finishes you can see something like: 
``` 
Smart Contracts Deployed to: 0x3F02Eeef513...e2a437d9cB5
```
🎉 Congrats! you have successfully Deployed your **Smart Contracts** to a test network. ✅

### If you are getting any error then Try this:
> First delete the artifacts and cache folder.

> Make sure your **Solidity file name** and **contracts Name** is same. e.g. File name: **Transactions.sol** and contract name: **contract Transactions { ..... }**

> Then run the below command.

```sh
npx hardhat compile
```
> This will definitely work and now you can be able to deploy it. ✅

That's not it. There is somthing more....
Now you have deployed your smart contracts to Goerli TestNet. Then you have to push and fetch data trom that contracts, Right!

So there is something more to know.
- After successful deployment copy the deployment address.
- Go to **clients/src** and make a folder called utils.
- then go to **clients/src/utils** and make a file called constants.js.

You should know that before deployment hardhat compiles the solidity code. And after successful compilation there is something that is automatically generated. it is called **ABI(Application Binary Interface)**. We need that ABI to push and fetch data from smart contracts.

You can find the ABI at: **smart_contracts/artifacts/contracts/Transactions.sol/Transactions.json**

- Copy the file and go to **clients/src/utils** and paste there.
- Now paste the below code to constants.js.

```js
import ABI from './Transactions.json';

export const contractABI = ABI.abi;
export const contractAddress = "0x3F02Eeef513...e2a437d9cB5";
```

Now you are ready to write code to connect **Smart Contracts** and **Nodejs**.

Thank you! CodeLek Team.

## License

**MIT**
