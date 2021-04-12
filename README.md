
# D'Cart 

This is a cart example using svelte and tailwind, the DApp is made with ethers library.

Clone the repository and run.

```bash
git clone https://github.com/stevepabatao/shopping-cart.git
cd <to the directory>
npm install
npm run dev
```

*Note that you will need to have [Node.js](https://nodejs.org) installed.*


## How to install Tailwind and Svelte


Installing tailwind and svelte

Create the project and install
```bash
npx degit sveltejs/template shopping-cart
cd <project_name>
npm install
```

Install Dependencies
```bash
npm install tailwindcss postcss autoprefixer svelte-preprocess postcss-load-config
```

Make tailwind and post css config files.

```bash
npm tailwindcss init -p
```

will create
   tailwind.config.js
   postcss.config.js

Add to rollup.config.js plusgins section

```javascript
preprocess: sveltePreprocess({
       sourceMap: !production,
       postcss: {
	plugins: [				         require('tailwindcss'),
	         require('autoprefixer'),
	],
       },
}),
```

Add this to App or create a seperate file and import it.

```html
<style global lang="postcss">
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
</style>
```

```bash
npm run dev
```
#Enable json on the 

Navigate to [localhost:5000](http://localhost:5000). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.


If you're using [Visual Studio Code](https://code.visualstudio.com/) we recommend installing the official extension [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode). If you are using other editors you may need to install a plugin in order to get syntax highlighting and intellisense.

## Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com) and [Netlify](https"//netlify.com).

## How to deploy and run a smart contract for demo

Clone the hackathon-boilerplate-project sample  on hardhat follow the instructions here.

```bash
https://hardhat.org/tutorial/hackathon-boilerplate-project.html
```

In this example you deploy and run a contract using the hardhat network

## How to run the hardhat network and deploy a conract.

Run the hardhat network

```bash
cd hardhat-hackathon-boilerplate/

npx hardhat node
```

Depoy the smart contract

```bash
npx hardhat --network localhost run scripts/deploy.js
```

You can get eth from the hardhat faucet for testing.

ex.

```bash
$ npx hardhat --network localhost faucet 0x0987a41e73e69f60c5071ce3c8f7e730f9a60f90
Transferred 1 ETH and 100 tokens to 0x0987a41e73e69f60c5071ce3c8f7e730f9a60f90
```

## Some notes to consider

Svelte by default does not support json and you will get errors if not configured. You need to activate json on rollup to run the application.

Open rollup.config.js and insert the line inside the plugins section

```javascript
plugins: [
---- some config here ----
       json(),
---- some config here ----
]
```

## How to deploy on a test network (ROPSTEN)

To deploy using hardhat, update the hardhat.config.js and add the following.

```javascript
require("@nomiclabs/hardhat-waffle");

require("./tasks/faucet");

const ALCHEMY_API_KEY = "<ALCHEMY_KEYS>";

const ROPSTEN_PRIVATE_KEY = "<ROPSTEIN_PRIVATE_KEY>";

module.exports = {
  solidity: "0.7.3",
  networks: {
    ropsten: {
      url: `https://eth-ropsten.alchemyapi.io/v2/${ALCHEMY_API_KEY}`,
      accounts: [`0x${ROPSTEN_PRIVATE_KEY}`]
    }
  }
};
```

Deploy the smart contract on the ropsten network

```bash
npx hardhat run scripts/deploy.js --network ropsten
```

Sample app running on netlify.

```bash
https://pensive-meninsky-b81ade.netlify.app/
```

