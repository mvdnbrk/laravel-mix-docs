# Installation

Though Laravel Mix is optimized for Laravel usage, it may be used for any type of application.

### Laravel Project

Laravel ships with everything you need to get started. Simply:

-   Install Laravel
-   Run `npm install`
-   Visit your `webpack.mix.js` file, and get started!

Now, from the command line, you may run `npm run watch` to watch your files for changes, and then recompile.

> {note} You won't find a `webpack.config.js` file in your project root. By default, Laravel defers to the config file from this repo. However, should you need to configure it, you may copy the file to your project root, and then update your `package.json` NPM scripts accordingly: `cp node_modules/laravel-mix/setup/webpack.config.js ./`.

### Stand-Alone Project

Begin by installing Laravel Mix through NPM or Yarn, and then copying the example Mix file to your project root.

```bash
mkdir my-app && cd my-app
npm init -y
npm install laravel-mix --save-dev
cp node_modules/laravel-mix/setup/webpack.mix.js ./
```

You should now have the following directory structure:

-   `node_modules/`
-   `package.json`
-   `webpack.mix.js`

The `webpack.mix.js` file is your configuration layer on top of webpack.  
Most of your time will be spent here.

Head over to your webpack.mix.js file:

```js
const mix = require('laravel-mix');

mix.js('src/app.js', 'dist')
   .sass('src/app.scss', 'dist')
   .setPublicPath('dist');
```

Take note of the source paths. You're free to amend the paths to match your preferred structure, but if you're happy with our defaults simply run `mkdir src && touch src/app.{js,scss}` to create the files/directories.  
You're all set now.  
Compile everything down by running `node_modules/.bin/webpack` from the command line.

You should now see:

-   `dist/app.css`
-   `dist/app.js`
-   `dist/mix-manifest.json` (Your asset dump file, which we'll discuss later.)

Nice job! Now get to work on that project.

#### NPM Scripts

As a tip, consider adding the following NPM scripts to your `package.json` file, to speed up your workflow. Laravel installs will already include this.

```js
"scripts": {
    "dev": "npm run development",   
    "development": "cross-env NODE_ENV=development run-s mix",
    "watch": "cross-env NODE_ENV=development run-s \"mix --watch\"",
    "hot": "cross-env NODE_ENV=development webpack-dev-server --inline --hot --config=node_modules/laravel-mix/setup/webpack.config.js",   
    "prod": "npm run production",
    "production": "cross-env NODE_ENV=production run-s mix",
    "mix": "webpack --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js"
}
```

To handle different environments, these scripts make use of [cross-env](https://www.npmjs.com/package/cross-env) and [npm-run-all](https://www.npmjs.com/package/npm-run-all):

```bash
npm install cross-env npm-run-all --save-dev
```
