
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

```bash
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

```bash
<style global lang="postcss">
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
</style>
```

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.


If you're using [Visual Studio Code](https://code.visualstudio.com/) we recommend installing the official extension [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode). If you are using other editors you may need to install a plugin in order to get syntax highlighting and intellisense.

## Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com) and [Netlify]().

