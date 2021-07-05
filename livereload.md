# LiveReload

While Laravel Mix ships with Browsersync support out of the box, you may prefer to use LiveReload. LiveReload can automatically monitor your files for changes and refresh the page when a modification is detected.

### Step 1. Install webpack-livereload-plugin

```bash
npm install --save-dev @kooneko/livereload-webpack-plugin

```

### Step 2. Configure `webpack.mix.js`

Add the following lines to the bottom of your webpack.mix.js:

```js
var LiveReloadWebpackPlugin = require('@kooneko/livereload-webpack-plugin');

mix.webpackConfig({
    plugins: [new LiveReloadWebpackPlugin()]
});
```

Although LiveReload works well with its defaults, a list of available plugin options may be reviewed [here](https://github.com/statianzo/webpack-livereload-plugin/blob/master/README.md).

### Step 3. Install LiveReload.js

Finally, we need to install LiveReload.js. You may do so via the [LiveReload Chrome plugin](https://chrome.google.com/webstore/detail/livereload/jnihajbhpnppcggbcgedagnkighmdlei),
or by adding the following code just before the closing `</body>` tag within your layout file.

```blade
    @env('local')
        <script src="http://localhost:35729/livereload.js"></script>
    @endenv
```

### Step 4. Run the Dev Server

```bash
npx mix watch
```

Now, LiveReload will automatically monitor your files and refresh the page when necessary. Enjoy!
