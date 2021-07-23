---
theme: seriph
highlighter: shiki
download: true
layout: image-right
themeConfig: {'primary': '#41B883'}
image: /img/vue-logo.svg
class: 'flex flex-col justify-center'
title: 'Vue & Nuxt - SSAST 2021 Summer Codecamp'
---

# Vue.js & Nuxt.js

Frontend Made Declarative

---

## What is Vue.js

<v-clicks>

- Progressive Framework for building UI
- Declarative Rendering, MVVM
- Components

</v-clicks>

---
layout: center
---

<iframe height="300" style="width: 600px;" scrolling="no" title="" src="https://codepen.io/panda2134/embed/XWRaReM?default-tab=js%2Cresult&theme-id=dark&editable=true" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/panda2134/pen/XWRaReM">
  </a> by panda2134 (<a href="https://codepen.io/panda2134">@panda2134</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

Change `message` in `data` and see what happens.

---

## MVVM

- Apply all modifications of data to the ViewModel
- The view code, i.e. DOM Tree, will update accordingly

```js
new Vue({ // create the ViewModel
  el: '#app', // mount the Vue app at #app
})
```

<v-click>

<div class="grid items-center justify-center m-5 leading-relaxed text-lime-500">
  <div>
    v-if, v-show, v-for, v-on,<br/>
    v-bind, v-model, v-text, v-html,<br/>
    v-cloak, ...
  </div>
</div>

</v-click>

---

## Template & Directives

<style>
  iframe {
    margin: 16px auto;
  }
</style>

<v-clicks>

- `{{ '{' + '{' + ' variableName ' + '}' + '}' }}` interpolate variable into your HTML code. (`v-text` is similar)
- `<div v-if="cond">Test</div>` only rendered when `cond` is a truthy value.
  - otherwise, the element is taken away from the DOM tree.
- `<div v-show="cond">Test</div>` set `display: none;` when cond is a falsy value.

</v-clicks>

<v-click v-after>

<iframe height="300" style="width: 600px;" scrolling="no" title="" src="https://codepen.io/panda2134/embed/XWRaReM?default-tab=js%2Cresult&theme-id=dark&editable=true" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/panda2134/pen/XWRaReM">
  </a> by panda2134 (<a href="https://codepen.io/panda2134">@panda2134</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

</v-click>


---

Sometimes we want to declare methods in a Vue instance, which can be then used in event callbacks, etc.

Declare them in the `methods` property:

```js
new Vue({
  el: '#app', // currentVal is then injected into `this`
  data: { currentVal: 1 },
  methods: {
    increaseBy (difference) { this.currentVal += difference }
  }
})
```

<v-click>

At times, we need to compute a property whose value is based on items in `data`, while maintaining reactivity, i.e. its value will update accordingly if one of its dependency changes. Use `computed` for this, and use `plusTwo` in the template like a normal data property.

```js
new Vue({
  el: '#app', // currentVal is then injected into `this`
  data: { currentVal: 1 },
  computed: { // will be updated when `currentVal` changes. otherwise the cached value will be used.
    plusTwo () { return this.currentVal + 2 }
  }
})
```

</v-click>

---

<v-click>

Use `v-on` to listen on events. `v-on:click` is equivalent to `@click`.

```html
<button v-on:click="handleClick">Click Me</button> <!--name of callback function-->
<button v-on:click="counter += 1">Click Me</button> <!--a single statement-->
```

</v-click>

<v-click>

### Have a try!

<iframe height="300" style="width: 100%; margin-top: 16px;" scrolling="no" title="Vue-Intro-0" src="https://codepen.io/panda2134/embed/PomjoQm?default-tab=js%2Cresult&editable=true&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/panda2134/pen/PomjoQm">
  Vue-Intro-0</a> by panda2134 (<a href="https://codepen.io/panda2134">@panda2134</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

</v-click>

---

Use `v-for` to implement a loop in templates. In the following code, `list` is an array declared in data.

```html
<div id="app">
  <ul>
    <li v-for="x in list">{{ x }}</li>
  </ul>
</div>
```

```js
new Vue({
  el: '#app',
  data: { list: [9, 8, 7] }
})
```


<v-click>

...will be rendered as:

```html
<div id="app">
  <ul>
    <li>9</li><li>8</li><li>7</li>
  </ul>
</div>
```

When `list` is modified, the corresponding parts in HTML are also re-rendered.

</v-click>

---

<v-clicks>

Use `v-bind` to bind an attribute to the view model. When the data in view model is modified, the attribute with `v-bind` will also be updated. (shorthand: `v-bind:prop="var"` ⇔ `:prop="var"`)

Use `v-model` on form elements (e.g. `<input>` and `<select>`) to bind the form element with a variable in `data`.

</v-clicks>

---

## How `v-model` works

<v-clicks>

- Edit the form element → `input` event triggered → data in view model changes
- Edit variable in view model → `value` attribute binded onto the variable → content in the element changes

</v-clicks>

<v-clicks v-after>

```html
<input v-model="text">
```

...is roughly equivalent to:

```html
<input :value="text" @change="handleChange">
```
and
```js
new Vue({
  el: '#app',
  data: { text: '' },
  methods: {
    handleChange(evt) {
      this.text = evt.target.value
    }
  }
})
```

</v-clicks>

---

## Have a try!

<iframe height="300" style="width: 100%; margin-top: 1rem" scrolling="no" title="Vue-Intro-1" src="https://codepen.io/panda2134/embed/eYWRYNK?default-tab=js%2Cresult&editable=true&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/panda2134/pen/eYWRYNK">
  Vue-Intro-1</a> by panda2134 (<a href="https://codepen.io/panda2134">@panda2134</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

---

## Single File Component

<v-clicks>

- Write HTML, CSS & JavaScript in a single `.vue` file.
- Used in `vue-cli` and Nuxt.js.
- Separated into 3 tags: `<template>` `<script>` & `<style>`

</v-clicks>

<v-click>

Example

<iframe height="300" style="width: 100%;" scrolling="no" title="TodoMVVM" src="https://codepen.io/panda2134/embed/MWydxVQ?default-tab=js%2Cresult&editable=true&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/panda2134/pen/MWydxVQ">
  TodoMVVM</a> by panda2134 (<a href="https://codepen.io/panda2134">@panda2134</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

</v-click>

---

## Composing with Components

<v-clicks>

- abstraction: application to tree of components
- components are small, self-contained and often reusable

![Components](https://vuejs.org/images/components.png)

</v-clicks>

---

### Encapsulation 

```html
<div> <!--From http://slides.com/sdrasner/intro-to-vue-3?token=LwIVIblm#/4/0/2-->
  <p></p>
  <div></div>
  <p></p>
  <small></small>
</div>
```

↓

```html
<call-out />
```

---

### Declaration of Components

<v-clicks>

- Components receive data from their parents via `props`, which is similar to attributes of HTML tags.
- They may also receive fragments of tags from parents, using `<slot></slot>`

</v-clicks>

<v-click>

### An example of <abbr title="Single File Component">SFC</abbr>

```vue
// hello-user.vue
<template>
  <span>Hello, {{ username }}</span>
</template>

<script>
export default {
  props: { username: String }
}
</script>
```

```vue
<template>
  <div><hello-user username="admin" /><!--you can also use v-bind:username--></div>
</template>
<script>
import HelloUser from './hello-user.vue'
export default {
  components: { HelloUser } // import and register the component
}
</script>
```

</v-click>

---

## `data` should be a function in components

Different from using `new Vue` directly, because each component has its own isolated scope.

```js
data: { a: 1 } // ❌ does not work as intended
data () { return { a: 1 } } // ✅ works
```


<iframe webkitallowfullscreen="" mozallowfullscreen="" allowfullscreen="" style="width:100%;height: 300px;" sandbox="allow-forms allow-scripts allow-popups allow-same-origin allow-pointer-lock allow-presentation" data-src="//codepen.io/sdras/embed/63d98696878200f6c0e987cd58341c39/?height=300&amp;theme-id=30324&amp;default-tab=html,result&amp;embed-version=2" allow="fullscreen" src="//codepen.io/sdras/embed/63d98696878200f6c0e987cd58341c39/?height=300&amp;theme-id=30324&amp;default-tab=html,result&amp;embed-version=2"></iframe>
<small>Thanks @sdras for her example!</small>

---

## One-way data flow

<blockquote>
All props form a one-way-down binding between the child property and the parent one: when the parent property updates, it will flow down to the child, but not the other way around. This prevents child components from accidentally mutating the parent’s state, which can make your app’s data flow harder to understand.
<small>(from Vue.js documentation)</small>
</blockquote>

<v-click>

→ **Never, ever** write to your `props` like this:
```vue
<script>
export default {
  props: { username: String },
  methods: {
    reverseUsername () { // ❌❌❌ Vue will give a warning in console
      this.username = this.username.split('').reverse().join('')
    }
  }
}
</script>
```

</v-click>
<v-click>

instead, copy `username` before use in `data`, and use the copied value instead:
```js
data () { // ✅
  return { usernameVal: this.username }
}
```

</v-click>

---

### Using slots

```html
<navigation-link url="/profile">
  <font-awesome-icon name="user"></font-awesome-icon>
  Your Profile
</navigation-link>
```

and in `NavigationLink.vue`:

```html
<a
  v-bind:href="url"
  class="nav-link"
>
  <slot></slot>
</a>
```

Upon rendering, the `<slot />` will be replaced with the icon and `Your Profile`.

---

### Compilation Scope

> **Everything in the parent template is compiled in parent scope; everything in the child template is compiled in the child scope.**

```html
<navigation-link url="/profile">
  Logged in as {{ user.name }} <!-- ✅ since user is defined in parent component -->
</navigation-link>
<navigation-link url="/profile">
  Clicking here will send you to: {{ url }} <!-- ❌ url is undefined -->
</navigation-link>
```

<v-click>

### fallback content

```html
<a>
  <slot>Nothing provided. This is the fallback content!</slot>
</a>
```

</v-click>

<v-click>

### named slots

A `<slot>` outlet without name implicitly has the name “default”.

```html
<div class="container">
  <header> <slot name="header"></slot> </header>
  <main> <slot></slot> </main>
  <footer> <slot name="footer"></slot> </footer>
</div>
```

</v-click>

---

then use the `v-slot` directive on a `<template>` to provide some content in parent components:

```html
<base-layout>
  <template v-slot:header>
    <h1>Here might be a page title</h1>
  </template>

  <p>A paragraph for the main content.</p>
  <p>And another one.</p>

  <template v-slot:footer>
    <p>Here's some contact info</p>
  </template>
</base-layout>
```

<v-click>

<blockquote>

You may also write:

```html
<template v-slot:default>
  <p>A paragraph for the main content.</p>
  <p>And another one.</p>
</template>
```

</blockquote>

</v-click>

---

## A brief review on shorthands

<table>
  <thead>
    <tr>
      <th>Original Form</th>
      <th>Shorthand form</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><samp>v-bind:value="var"</samp></td>
      <td><samp>:value="var"</samp></td>
    </tr>
    <tr>
      <td><samp>v-on:input="callback"</samp></td>
      <td><samp>@input="callback"</samp></td>
    </tr>
    <tr>
      <td><samp>v-slot:header</samp></td>
      <td><samp>#header</samp></td>
    </tr>
  </tbody>
</table>

---

## Custom events

In methods of Vue instance, you may use `this.$emit` to fire up custom events;
this can be useful if you want to pass something from the component back to its parent.

```js
this.$emit('change', this.val)
```

---

## Nuxt.js

<v-clicks>

- Bundler is needed for Single File Components, because `.vue` files aren't natively understood by browsers.
- Webpack + [`vue-loader`](https://vue-loader.vuejs.org/) is usually used.
  - Recall: loaders are used for source transformation, importing assets, etc.
- The official solution is [`@vue/cli`](https://cli.vuejs.org/), however you need to deal with [`vue-router`](https://router.vuejs.org/) and [`vuex`](https://vuex.vuejs.org/) all yourself.
- Nuxt.js handles routing and state management for you, with server-side rendering enabled and more

</v-clicks>

---

### What is Server-Side Rendering

- Some content is rendered on the server side, and the rendered version, along with page logic code, is sent to clients.
- Crucial for SEO because some crawlers cannot run JavaScript. Without SSR, they'll crawl blank pages.

<v-click>

### What Nuxt.js can do

</v-click>

<v-clicks>

- automatically generates the `vue-router` configuration
- server-side rendering & static sites
  - difference: for static sites, all pages are rendered at **build time**.
- better data fetching, other than the traditional approach using `mounted()` hook
  - fetch data with `asyncData(ctx)` or `fetch()` hook to get correct SSR results
- builtin loading progress bar support (also used by [axios module](https://axios.nuxtjs.org/))

</v-clicks>

---

### Create a basic Nuxt.js project

Reference: https://nuxtjs.org/docs/2.x/get-started/installation

```bash
$ yarn create nuxt-app nuxt-example
$ cd nuxt-example
$ yarn dev
```

<v-click>

<img src="/img/nuxtjs.png" alt="Nuxt Initial Page" height="600">

</v-click>

---
layout: two-cols
---

### Directory Structure

<img src="/img/file-structure.png" alt="Nuxt Directory Structure" style="height:60vh;">

::right::

If any of these folders is missing, create them.

<v-clicks>

- components: all your Vue.js components (SFCs) which are then imported into your pages.
- pages: application's views. routes are generated automatically.
- assets: uncompiled assets such as your styles, images, or fonts.
- static: directly mapped to the server root and contains files that have to keep their names (e.g. `robots.txt`) or likely won't change (e.g. the favicon)
- plugins: usually used for Nuxt.js plugins
- store: Vuex store files. Vuex is enabled only if `store/index.js` is present.
- nuxt.config.js: configuration for Nuxt.js

</v-clicks>

<!--
Show 'em in a real Nuxt.js project
-->

---

## `context` in Nuxt.js

<v-clicks>

- a `context` per page load / router push
- contains router params, Vuex store, Nuxt.js contents, etc.

</v-clicks>

<v-click>

<img src="https://nuxtjs.org/docs/2.x/context.svg" alt="Nuxt Context" style="height: 50vh">

</v-click>

---

<v-clicks>

- `context` is different from Vue.js instance object (`this`)
  - read the docs carefully. In some hooks (like `asyncData`) only `context` can be used.
- `ctx.app` is the **root** Vue instance
- `ctx.store` is Vuex store instance
  - `ctx.store.state`, `ctx.store.dispatch`, `ctx.store.commit`
- <samp>ctx.<mark>route</mark></samp> is `vue-router` instance
- `ctx.params`: router params, like `id` in `pages/posts/_id.vue`
  - alias of `ctx.route.params`
- `ctx.query`: router query, i.e. parsed query string
  - query string: the `?a=1&b=2` part of URL (note: it should be [encoded](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent))

</v-clicks>

---

<v-clicks>

- some components are also injected into `this`, but `this` is not always available
- `this.$route` by Vue Router
- `this.$store` by Vuex (if enabled)
- `this.$content` by [Nuxt Content](https://content.nuxtjs.org/)

</v-clicks>

---

## Using Life-Cycle Hooks and Nuxt.js Context

### Vue.js Life Cycle Hooks

<div style="height: 55vh; overflow-x: scroll; border: 1px solid #ccc;">
  <img src="https://vuejs.org/images/lifecycle.png" alt="Vue.js LifeCycle">
</div>

---

Vue.js projects usually make calls to API in `mounted()` hook

<v-click>

```js
export default {
  data () {
    return { currentWeather: null }
  },
  async mounted () {
    const res = await fetch('https://example.com/weather.json')
    this.currentWeather = await res.json()
  }
}
```

</v-click>

<v-click>

For Nuxt.js projects, `asyncData(ctx)` and `async fetch()` is preferred, since they're designed for SSR.

```html {monaco}
<template>
  <p v-if="$fetchState.pending">Fetching mountains...</p>
  <p v-else-if="$fetchState.error">An error occurred :(</p>
  <div v-else>
    <h1>Nuxt Mountains</h1>
    <ul>
      <li v-for="mountain of mountains">{{ mountain.title }}</li>
    </ul>
    <button @click="$fetch">Refresh</button>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        mountains: []
      }
    },
    async fetch() {
      this.mountains = await this.$axios.$get( // using [axios module](axios.nuxtjs.org)
        'https://api.nuxtjs.dev/mountains'
      )
    }
  }
</script>
```

</v-click>

<style>
iframe {
  height: 30vh !important;
  overflow: scroll;
}
</style>

<!--
Explain the new fetch hook in details
-->

---

```js
export default {
  async asyncData({ params }) {　// gettings `params` from nuxt context
    const { data } = await axios.get(`https://my-api/posts/${params.id}`)
    return { title: data.title } // replaced the good old `data` method
  }
}
```

---

### Nuxt.js Life Cycle Hooks

https://s3-ap-southeast-2.amazonaws.com/kruties-diagrams/nuxtjs/NuxtJs_Lifecycle_Hooks.pdf

---

## Example project using fetch

https://codesandbox.io/s/github/nuxtlabs/examples/tree/master/data-fetching/fetch-hook?from-embed

---

## References

- <logos-vue class="inline"/> [Vue.js Official Document](https://vuejs.org/)
- <logos-nuxt-icon class="inline"/> [Nuxt.js Official Document](https://nuxtjs.org/), with in-depth explanation of internal structure
- <ic-sharp-download class="inline" /> [Nuxt Axios Module](https://axios.nuxtjs.org/)
- <ant-design-file-markdown-filled class="inline" /> [Nuxt Content](https://content.nuxtjs.org/)
  - Read the docs thoroughly before doing your homework

## Homework

- Make your own static blog generator!
- Don't worry, most of the code is written for you, you only need to fill in the blanks in the code.

---

![Homework Index Page](/img/homework.png)