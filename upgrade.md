# Upgrade to v4.0

```bash##
npm remove laravel-mix
npm install laravel-mix@4.0.0
```

After upgrading, if you encounter any issues related to `vue-template-compiler`, this is related to the fact that your installed version numbers of vue and `vue-template-compiler` must be identical. Update one or both to fix this issue.

## New

-   Faster compiles
-   Faster npm installs.
-   Upgraded to webpack 4   
-   Upgraded to vue-loader 15
-   Upgraded to Babel 7
-   Automatic vendor extraction. If you call `mix.extract()` with zero arguments, all vendor dependencies (any package from `node_modules/` that you pull in) will automatically be extracted. Nifty!
-   CSS minification (via cssnano) options may be provided 887808f
-   PostCSS plugins may be passed to mix.sass/less/stylus() on a per-call basis. This means you may provide unique PostCSS plugins for each `mix.sass()` call, if desired.
-   Switched JS optimizing/minification from Uglify to Terser.
-   Switched from node-sass to Dart Sass. While this comes with a small increased compile-time cost, the benefit is faster and more reliable npm installs.
-   Improved Babel config merging strategy. You may now override or tweak any default Babel plugins and presets provided through Mix by creating a `.babelrc` file in your project root.

## Fixed

-   All npm audit alerts have been fixed, thanks to the upgrade to webpack 4.

## Notes

-   If your project heavily uses JavaScript dynamic imports, you may need to hold off until the release of webpack 5 early next year. There are known compile issues related to this that we cannot fix until then. Once webpack 5 is out, Mix will be updated shortly after. **If you're unfamiliar with dynamic imports, then this very likely won't affect your project**.
-   Sass support is now an on-demand dependency. In prior versions of Mix, the `node-sass` and `sass-loader` dependencies were included out of the box, regardless of whether your project required Sass compilation or not. To help improve install times, these two dependencies will now be installed on-demand if, and only if, your project specifies Sass compilation with `mix.sass()`. The first time you run npm run dev, the dependencies will be installed and saved to your dev-dependencies list.

## Importing ES Modules

As part of the vue-loader 15 updates, if your code uses the CommonJS syntax for importing EcmaScript modules, you'll need to append `.default`, like so:

```js
Vue.component('example-component', require('./components/ExampleComponent.vue').default);
```

Switching to EcmaScript imports is the **recommended** option:

```js
import ExampleComponent from './components/ExampleComponent.vue';

Vue.component('example-component', ExampleComponent);
```

## Babel 7 support

1.  The naming convention for official Babel plugins has changed. They are now scoped under the @babel namespace. As such, in your package.json file, change all occurrences of `"babel-plugin-[name]": "6.x"` to `"@babel/plugin-[name]": "7.x"`.
2.  If you've created a `.babelrc` file in your project, update all plugin name references. For example, update `"plugins": ["babel-plugin-transform-object-rest-spread"]` to `"plugins": ["@babel/plugin-proposal-object-rest-spread"]`.

## Switch from Node Sass to Dart Sass

As part of our switch from `node-sass` to `dart-sass`, though support is largely identical, you may notice changes or warnings upon compilation. You may either address these one-by-one, or you can manually switch back to node-sass, like so:

```bash
npm install node-sass
```

```js
mix.sass('resources/sass/app.sass', 'public/css', {
    implementation: require('node-sass')
});
```

## Removed fastSass() and standaloneSass()

`mix.fastSass()` and `mix.standaloneSass()` (aliases) have been removed entirely.  
In an effort to improve performance for those who only need to compile CSS, this command provided Sass compilation that was separate from the core webpack build.  
However, it seems to be more confusing than helpful to newcomers.  
Migrate by switching from `mix.fastSass()` to `mix.sass()`.

## Removed deprecated `.mix` property

The deprecated mix property has now been removed.  
If you have `require('laravel-mix').mix` in your webpack.mix.js file, change it to `require('laravel-mix')`.

## Switch from Uglify to Terser

Due to the mandatory switch from Uglify to Terser, if your project was overriding the default config with `Config.uglify = {}`, you'll need to switch to `Config.terser = {}`.  
The [options API](https://github.com/webpack-contrib/terser-webpack-plugin#terseroptions) is largely the same.

**Before:**

```
// webpack.mix.js

mix.options({
    uglify: {
        uglifyOptions: {
            warnings: true
        }
    }
});
```

**After:**

```
mix.options({
    terser: {
        terserOptions: {
            warnings: true
        }
    }
});
```

## Vue component Sass preprocessing

If your project does not include a `mix.sass()` call (which automatically downloads all necessary dependencies), but does specify `lang="sass"` in your Vue components, you may need to install either node-sass or sass.  
Because Mix doesn't know which preprocessors you specify in your Vue components, you'll need to manually pull them in.  
You can fix this with `npm install node-sass sass-loader` or `npm install sass sass-loader`.  
Please note that the same is true for Less and Stylus.
