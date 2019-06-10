# jQuery UI

jQuery UI is a toolkit for rendering common components, such as datepickers, draggables, etc. No adjustments are needed to make it work with Laravel Mix.

## Build your `webpack.mix.js` configuration

```js
mix.js('resources/js/app.js', 'public/js')
   .sass('resources/sass/app.scss', 'public/css');
```

## Install `jquery-ui`

```bash
npm install jquery-ui --save-dev
```

## Load your desired widget

```js
// resources/js/app.js

import $ from 'jquery';
window.$ = window.jQuery = $;

import 'jquery-ui/ui/widgets/datepicker.js';
```

## Load CSS

```css
// resources/sass/app.scss

@import '~jquery-ui/themes/base/all.css';
```

## Trigger the UI Plugin

```js
// resources/js/app.js

$('#datepicker').datepicker();
```
