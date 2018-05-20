---
sidebar: auto
---

# Guide

In the following sections you will learn how to use the components directly with a CDN (Content Delivery Network) or to bundle them with a bundler e.g. webpack to build more complex projects. 

::: tip
Each approach depends on what you are targeting. When you want to integrate just some small components in your existing library I recommend you to use the CDN way. When you want to setup a whole project to use these material components then it would be the best to be familiar with a bundler of your choice and taking the compiling way.
:::

## CDN Usage

Integrating a component e.g. Button is quite easy:

```html
<html>
  <head>
    <link rel="stylesheet"
      href="https://cdnjs.com/libraries/normalize">
    <link rel="stylesheet"
      href="https://fonts.googleapis.com/css?family=Roboto:300,400,500" type="text/css">
    <link rel="stylesheet"
      href="https://fonts.googleapis.com/icon?family=Material+Icons">
    <link rel="stylesheet"
      href="https://unpkg.com/material-components-vue/dist/typography/typography.min.css">
    <link rel="stylesheet"
      href="https://unpkg.com/material-components-vue/dist/button/button.min.css">
  </head>
  <body>
    <div id="app">
      <m-typography>
        <m-button>Example</m-button>
      </m-typography>
    </div>
    <script src="https://unpkg.com/vue"></script>
    <script
      src="https://unpkg.com/material-components-vue/dist/typography/typography.min.js">
    </script>
    <script
      src="https://unpkg.com/material-components-vue/dist/button/button.min.js">
    </script>
    <script>
      const app = new Vue({
        el: '#app'
      })
    </script>
  </body>
 </html>
```

### Theming

#### Define Color System

To setup you own brand colors just integrate a Theme component in your template and pass in an object with CSS custom properties, but keep browser compatibilty in mind. For all a complete list of properties have a look [here](https://github.com/material-components/material-components-web/blob/master/packages/mdc-theme/README.md#css-custom-properties).

```html
<head>
  <link rel="stylesheet"
      href="https://unpkg.com/material-components-vue/dist/theme/theme.min.css">
</head>
<body>
  <m-theme :customStyle="material">
    <m-button>
      Example
    </m-button>
  </m-theme>
  <script>
    const app = new Vue({
      el: '#app',
      data() {
        return {
          material: {
            '--mdc-theme-primary':  '#5e35b1',
            '--mdc-theme-secondary': '#ff5722',
            '--mdc-theme-background': '#ffffff'
          }
        }
      }
    })
  </script>
</body>
```

#### Use Color System

For simple color modifications of components e.g. changing the background color from primary to secondary color it's possible to use the `theming` prop on each component to set one of the mdc-theme CSS classes.
You don't need to set the full name of the CSS class just the last part (see example). For a complete list of available 
CSS classes have a look [here](https://github.com/material-components/material-components-web/tree/master/packages/mdc-theme#css-classes).

All you have to do is to addtionally import the Theme stylesheet (reusing the above example) and set the `theming` prop on the component: 

```html
<head>
  <link rel="stylesheet"
      href="https://unpkg.com/material-components-vue/dist/theme/theme.min.css">
</head>
<body>
  <m-button theming="secondary-bg">
    Secondary-Button
  </m-button>
</body>
```

## Bundler Usage

::: warning
I assume that you have a working bundler setup e.g. generated by the [vue-cli](https://github.com/vuejs/vue-cli) thats capable of loading SASS stylesheets and Vue.js SFC (Single File Components).
:::

## Installation

```bash
npm install --save material-components-vue

# or with yarn
yarn add material-components-vue
```

## Import Components

```vue
<template>
  <m-button>Hello</m-button>
</template>

<script>
import Button from 'material-components-vue/dist/button'
Vue.use(Button)

export default {
  // ...
}
</script>

<style lang="scss">
  @import "material-components-vue/dist/button/styles";
</style>
```

## Using SASS Customizations

The original mdc-web components are implemented by using SASS to generate highly customizable stylesheets. SASS can be used to define e.g. custom colors on components or to modify the shape. Please inform yourself at each component subdirectory on the official repository to see what is possible with each component - see [here](https://github.com/material-components/material-components-web/tree/master/packages).

You will have direct access to all SASS stylesheets by importing them in your project files:

```vue
<style lang="scss">
  @import "material-components-vue/dist/theme/styles";
  @import "material-components-vue/dist/button/styles";
  @import "material-components-vue/dist/card/styles";
  // ...
</style>
```

Now you can modify SASS variables to establish your own brand colors:

```vue
<style lang="scss">
  $mdc-theme-primary: #2196f3;
  $mdc-theme-secondary: #ff1744;
  $mdc-theme-background: #f5f5f5;
  @import "material-components-vue/dist/theme/styles";
  @import "material-components-vue/dist/button/styles";
  @import "material-components-vue/dist/card/styles";
</style>
```
::: warning
Don't forget to include the `@material` directory of your `node_modules` in your sass-loader options.
Otherwise the components won't compile sucessfully.
:::