*Looking for a shareable component template? Go here --> [sveltejs/component-template](https://github.com/sveltejs/component-template)*

---

# svelte app

This is a project template for [Svelte](https://svelte.dev) apps. It lives at https://github.com/sveltejs/template.

To create a new project based on this template using [degit](https://github.com/Rich-Harris/degit):

```bash
npx degit sveltejs/template svelte-app
cd svelte-app
```

*Note that you will need to have [Node.js](https://nodejs.org) installed.*


## Get started

Install the dependencies...

Installing tailwind and svelte

npx degit sveltejs/template shopping-cart
cd <project_name>
npm install

npm install tailwindcss postcss autoprefixer

npm tailwindcss init -p
will create
   tailwind.config.js
   postcss.config.js

add to rollup.config.js plusgins section

preprocess: sveltePreprocess({
       sourceMap: !production,
       postcss: {
	plugins: [				         require('tailwindcss'),
	         require('autoprefixer'),
	],
       },
}),

npm install svelte-preprocess postcss-load-config

Add this to App or create a seperate file and import it.
<style global lang="postcss">
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
</style>


```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.

If you're using [Visual Studio Code](https://code.visualstudio.com/) we recommend installing the official extension [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode). If you are using other editors you may need to install a plugin in order to get syntax highlighting and intellisense.

## Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com).

