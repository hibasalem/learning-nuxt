

Nuxt.js is a free and open-source web application framework for Vue.js, a popular JavaScript framework for building user interfaces. Nuxt.js is designed to make it easy to create universal or server-side rendered (SSR) Vue.js applications.    


Nuxt.js simplifies the process of building Vue.js applications and provides a structured framework that is well-suited for projects of varying sizes and complexities. It is often used for building single-page applications (SPAs), static websites, and server-rendered applications.


#### Key features of Nuxt.js include:

- **Server-Side Rendering (SSR)**: Nuxt.js allows you to render Vue.js applications on the server side before sending the HTML to the client. This can improve the initial loading performance and SEO of your web applications.

Vue Router Integration: Nuxt.js comes with Vue Router pre-configured, making it easy to set up routes for your application.

- **Vuex Integration**: Nuxt.js also integrates with Vuex, which is the state management library for Vue.js. This helps manage the state of your application in a predictable and centralized way.

- **Automatic Code Splitting**: Nuxt.js automatically splits your code into smaller chunks, helping to optimize the loading performance of your application.

- **Static Site Generation (SSG)**: In addition to SSR, Nuxt.js supports static site generation, where the pages can be pre-rendered at build time and served as static HTML files. This is beneficial for websites with content that doesn't change frequently.

- **Middleware**: Nuxt.js provides middleware functionality, allowing you to run code on the server or the client before rendering a page.

- **Plugin System**: Nuxt.js has a flexible plugin system that enables you to easily extend and configure the functionality of your application.


#### get started

- npx nuxi@latest init <project-name>
- cd <project-name>
- npm run dev


## Pages:

- Pages in Nuxt.js represent the individual views or routes of your application.

- Each .vue file in the pages directory corresponds to a specific route in your application.

- You can define the layout for a specific page directly within that page file using the layout property.

```vue

<!-- pages/index.vue -->
<template>
  <div>
    <h1>This is the home page</h1>
  </div>
</template>

<script>
export default {
  layout: 'default', // Layout for this specific page
}
</script>
```
## Layouts

- Layouts in Nuxt.js are reusable components that define the overall structure of your pages.
- They typically include common elements such as headers, footers, navigation bars, etc.
- You can define a default layout that is applied to all pages unless overridden by a specific page.

```vue

<!-- layouts/default.vue -->
<template>
  <div>
    <header>
      <!-- Header content -->
    </header>
    <main>
      <nuxt /> <!-- This is where the content of the page will be rendered -->
    </main>
    <footer>
      <!-- Footer content -->
    </footer>
  </div>
</template>

<script>
export default {
  // Layout-specific logic can be defined here
}
</script>

```


#### Advantages of Using Layouts:

- Reusability: Layouts allow you to create a consistent structure across multiple pages.
- Maintainability: If you need to make changes to the overall structure of your application, you can do it in one central place (the layout) instead of updating each individual page.
- Organization: Separating layout concerns from individual pages helps in keeping your codebase organized and modular.

-----------------

## Assets 

assests file vs puplic ??

## composables

Composables in Vue.js are a way to organize and encapsulate logic that can be reused across components. They are usually functions that return data, methods, or computed properties, making it easy to share functionality among different parts of your application.

 sharing logic between components, composables can also be used to share logic between pages and other parts of your Nuxt. js application
 
```vue 
 <script setup lang="ts">
const foo = useFoo()
</script>

<template>
  <div>
    {{ foo }}
  </div>
</template>
```

## blugins 

Nuxt has a plugins system to use Vue plugins and more at the creation of your Vue application. Nuxt automatically reads the files in the plugins/ directory and loads them at the creation of the Vue application. All plugins inside are auto-registered, you don't need not add them to your nuxt.config separately.


```vue 
<!-- nuxt.config.ts -->
export default defineNuxtConfig({
  plugins: [
    '~/plugins/bar/baz',
    '~/plugins/bar/foz'
  ]
})```

```vue 
export default defineNuxtPlugin(nuxtApp => {
  // Doing something with nuxtApp
})
```

## middleware directory 

Nuxt provides a customizable route middleware framework you can use throughout your application, ideal for extracting code that you want to run before navigating to a particular route.   

There are three kinds of route middleware:
- Anonymous (or inline) route middleware are defined directly within the page.
- Named route middleware, placed in the middleware/ and automatically loaded via asynchronous import when used on a page.
- Global route middleware, placed in the middleware/ with a .global suffix and is run on every route change.

```ts 
export default defineNuxtRouteMiddleware((to, from) => {
  if (to.params.id === '1') {
    return abortNavigation()
  }
  // In a real app you would probably not redirect every route to `/`
  // however it is important to check `to.path` before redirecting or you
  // might get an infinite redirect loop
  if (to.path !== '/') {
    return navigateTo('/')
  }
})
```


Middleware runs in the following order:
1. Global Middleware , By default, global middleware is executed alphabetically based on the filename.

2. Page defined middleware order (if there are multiple middleware declared with the array syntax)

## modules 

Nuxt modules are async functions that sequentially run when starting Nuxt in development mode using nuxi dev or building a project for production with nuxi build . They can override templates, configure webpack loaders, add CSS libraries, and perform many other useful tasks.

## state management  
Nuxt provides powerful state management libraries and the useState composable to create a reactive and SSR-friendly shared state.

we can use Pinia module to create a global store and use it across the app.

## server 

there is api and routes folders to provide endpoints , we can add the methods as prefix `x.get.js` 

## Nitro 


## Rendering Modes
Both the browser and server can interpret JavaScript code to turn Vue.js components into HTML elements. This step is called rendering. Nuxt supports both universal and client-side rendering. The two approaches have benefits and downsides 
   
By default, Nuxt uses universal rendering to provide better user experience, performance and to optimize search engine indexing, but you can switch rendering modes in one line of configuration.


## Data fetching

Nuxt comes with two composables and a built-in library to perform data-fetching in browser or server environments: useFetch, useAsyncData and $fetch

- `useFetch` is the most straightforward way to handle data fetching in a component setup function.
- `$fetch` is great to make network requests based on user interaction.
- `useAsyncData`, combined with $fetch, offers more fine-grained control.

## SEO and Meta 

 Out-of-the-box, Nuxt provides sane defaults, which you can override if needed.
 
- using  `app.head` , This method does not allow you to provide reactive data.
```ts
export default defineNuxtConfig({
  app: {
    head: {
      charset: 'utf-8',
      viewport: 'width=device-width, initial-scale=1',
    }
  }
})
```

-The `useHead` composable function 
  -allows you to manage your head tags in a programmatic and reactive way   
```vue 
  <script setup lang="ts">
    useHead({
      title: 'My App',
      meta: [
        { name: 'description', content: 'My amazing site.' }
      ],
      bodyAttrs: {
        class: 'test'
      },
      script: [ { innerHTML: 'console.log(\'Hello world\')' } ]
    })
  </script>
```

- `useSeoMeta`

```vue 
<script setup lang="ts">
useSeoMeta({
  title: 'My Amazing Site',
  ogTitle: 'My Amazing Site',
  description: 'This is my amazing site, let me tell you all about it.',
  ogDescription: 'This is my amazing site, let me tell you all about it.',
  ogImage: 'https://example.com/image.png',
  twitterCard: 'summary_large_image',
})
</script>
```

- Components 

Nuxt provides `<Title>, <Base>, <NoScript>, <Style>, <Meta>, <Link>, <Body>, <Html> `and `<Head>` components so that you can interact directly with your metadata within your component's template.        
Because these component names match native HTML elements, it is very important that they are capitalized in the template.


#### in useHead we can add what ever 3rd party scripts we need , also in the app.head 

## Lifecycle Hooks
Nuxt provides a powerful hooking system to expand almost every aspect using hooks.


[https://nuxt.com/docs/api/advanced/hooks#nuxt-hooks-build-time](https://nuxt.com/docs/api/advanced/hooks#nuxt-hooks-build-time)
there is **Build Time** and  **Runtime**

- Nuxt Hooks (Build Time)     
Nuxt Modules and build context.    
Within `nuxt.config` and Within Nuxt Modules

- App Hooks (Runtime)
App hooks can be mainly used by Nuxt Plugins to hook into rendering lifecycle but could also be used in Vue composables.    
```vue
export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.hook('page:start', () => {
    /* your code goes here */
  })
})

```
- Server Hooks (Runtime)
These hooks are available for server plugins to hook into Nitro's runtime behavior.

- Additional Hooks


## configrations 

------------------------------
# Key Concepts

## Auto-imports

Nuxt can auto-import your `components/`, `composables/` and `utils/` and `server/utils/` ,,    

You can also auto-import functions exported from custom folders or third-party packages by configuring the `imports` section of your `nuxt.config` file.

#### Built-in Auto-imports

- Nuxt auto-imports functions and composables to perform data fetching, get access to the app context and runtime config, manage state or define components and plugins.

- Vue 3 exposes Reactivity APIs like ref or computed, as well as lifecycle hooks and helpers 

***Nuxt only includes what is used in your production code.***

- the composables that is Contrary to a classic global declaration, Nuxt preserves typings, IDEs completions and hints, and only includes what is used in your production code.
- in the same time we can import them and do customization 

When you are using the built-in Composition API composables provided by Vue and Nuxt, be aware that many of them rely on being called in the right context.
**If you get an error message like Nuxt instance is unavailable then it probably means you are calling a Nuxt composable in the wrong place in the Vue or Nuxt lifecycle.**

#### Directory-based Auto-imports 

- components/ for Vue components.   
- composables/ for Vue composables.    
- utils/ for helper functions and other utilities.     

-------------------------

we still can do Explicit Imports
```vue 
<script setup lang="ts">
import { ref, computed } from '#imports'

const count = ref(1)
const double = computed(() => count.value * 2)
</script>
```

#### Auto-import from third-party packages

```ts

export default defineNuxtConfig({
  imports: {
    presets: [
      {
        from: 'vue-i18n',
        imports: ['useI18n']
      }
    ]
  }
})

```