# System Notifications

By default, Laravel Mix will display a system notification for each compilation.  
That way, you can quickly see if you have any errors that need addressing.  
However, in certain circumstances, this is undesirable \(such as compiling on your production server\).
If this happens to be the case, they can be disabled from your `webpack.mix.js` file.

```js
mix.disableNotifications();
```

Maybe you only want to be notified if there are any errors? That is possible too, by only disabling
the success notifications. Please note that this is intended to be used via the `watch` command. 
The first compilation always displays a success notification. Only subsequent success notifications
are disabled.

```js
mix.disableSuccessNotifications();
```

Simple!
