# VUE Components

## Components 

Components are the building blocks It’s common for components to be “parents” that have child components nested within them.

A component is like a custom HTML-element. -> reuseable Pieces of HTML with connected Data and logic

- Components are used to build UIs by combining them
- reuse
- smaller pieces 
- Components build "parent-child" relations and use "unidirectional data flows" for communication

::: tip
Convention: 

- The Name Should be made up of 2 words

- start with capital-letter. 
- not the same name as a html-tag
- put in components-folder

:::

## Single File Components

`.vue` - files

A typical .vue component has three sections: `<template>`, `<script>`, and `<style>`.

Traditionally, these sections are written in HTML, JavaScript and CSS.

Use Pug, TypeScript and SCSS instead by adding the appropriate `lang` attributes.

```html
    <template lang="pug">
    </template>
    
    <script lang="ts">
    </script>
    
    <style lang="scss" scoped>
    </style>
```

> (Make sure you have the proper loaders setup and your Webpack is configured to handle these alternatives). 
>
> For example,  to use SCSS,  make sure to install sass-loader and its peer dependency node-sass:
>
> ```
> npm install --save-dev sass-loader node-sass
> ```
>
> Check out the [Vue Loader docs](https://vue-loader.vuejs.org/guide/pre-processors.html).
>

------

## Import Component

1. **Import**: (VSCode Snippet `vimport`) 

   ```js
   import EventCard from '@/components/EventCard.vue'
   ```

2. **register** this component as a child component (snippet `vcomponents`) 

   ```js
   components: {
   	EventCard
   }
   ```

   > because we’re using ES6, this is the same as:
   >
   > ```js
   > components: {
   > 	EventCard: Eventcard
   > }
   > ```

3. **use** in template (as if it were an HTML-tag)

   ```vue
   <template>
   	<EventCard />
   </template>
   ```

------

or

#### Register Component in `main.js`

`main.js`

```js
app.component('active-element', ActiveElement);
```

------

## Local vs Global Components

registering Components

### 1. Global Components:

```js
//main.js

const app = createApp(App);

app.component('user-info', UserInfo);

app.mount('#app');
```

Can be used anywhere in the whole app!

Downside: 

- they all have to be loaded initially. Problem in bigger apps
- list can get very long

### 2. Local Components

```js
import TheHeader from './components/TheHeader.vue';

export default {
  components: { 'the-header': TheHeader },
```

components-property wants an object with key-value pairs. key= name of the custom tag, value= the component

##### vue automatically translates between PascalCase and kebap-case

You can also write:

```
 components: { TheHeader: TheHeader },
```

`TheHeader` can be used in the template as: `the-header`

or as `<TheHeader />` (this can also be self-closing)

Simpler Syntax: (modern JS-Syntax)

```
components: { TheHeader }
```

------

## Styles

### `scoped` 

CSS is always global  - is applied to all components! (Usually you define global CSS in app.vue)

-> To just use it in the component add `scoped`-attribute to the style-tag

*scope* and isolate the styles to just this component. This way, these styles are specific to this component and won’t affect any other part of our application.

```vue
<style scoped >
header {
...
}
</style>
```

> under the Hood: vue gives the components special data-atributes
>
> ```
> header h1[data-v-9a9f6144] {...}	
> ```
>
> - vue adds data-attribute to html and css-selectors
>
> - -> performance-issues
>
> - -> sometimes it's better to just write a more specific css-selector !!
>
>   ```css
>   modal h1 {
>   	...
>   }
>   ```
>



### Global Styles

- Several different ways to handle this. The simplest way is to add styles to the **App.vue** file - the root component of our app.  
- It’s recommended to only store your global styles in one place to avoid potential conflicts.
- You can also place content in our **App.vue**’s template that you want to be displayed globally across every view of our application.


Don't scope the root-component. Use global Stylesheet `global.css` in assets folder (or `main.css`). Import in main.js

```js
import './assets/global.css'
```

