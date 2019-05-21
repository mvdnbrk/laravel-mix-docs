# Upgrade from v2.1 to v3.0

## Babel 7 support

As this new version of Babel [includes major breaking changes](https://babeljs.io/blog/2018/08/27/7.0.0#major-breaking-changes),  
Mix also needs to bump from v2 to v3.

We've taken care of most of the changes, however, if your project pulls in extra Babel plugins that Mix does not provide out of the box, you'll need to update locally as well.

The naming convention for official Babel plugins has changed.  
They are now scoped under the **@babel** namespace.  

Update your `package.json` and change all occurences of `"babel-plugin-[name]"`:

```diff
- "babel-plugin-[name]": "6.x"
+ "@babel/plugin-[name]": "7.x"
```

If you've created a `.babelrc` file in your project, update all plugin name references:  

```diff
- "plugins": ["babel-plugin-transform-object-rest-spread"]
+ "plugins": ["@babel/plugin-proposal-object-rest-spread"]
```
