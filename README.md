# vue-book

Tree view for your demo components. [Demo](http://vue-book.asva.by/#/Demo/ContactComponent.vue).

![Interface](docs/main.gif)

## Install

* **npm**: `npm install -D vue-book` 
* **yarn**: `yarn add -D vue-book`

## Features
* Display your components as a tree or flat list.
* Preview components on the page.
* Text search.
* Routing support.
* Saves on page reload.

## The gist

I'll talk a bit about demo based workflow I employ in my projects.

Before doing any work on component I create a demo. Demo allows me to define an interface, like this:
```html
<my-new-component v-model="dataItem" :some-prop="prop"/>
```
Only then I start to work on component.

You can think of demo as of semi-manual unit tests. But why not use actual unit tests, you'll ask. Let me explain.
* Demos are cheap. And you don't have to be a senior unit tester to create them.
* Demos are visual. In many cases you can *see* if something goes wrong. But unit tests won't show any of your styling mistakes.
* Demos are developer friendly. You can instantly find usage examples or just glance over existing components. Which is crucial for teamwork.

Of course, this doesn't mean that you have to dump unit tests. Just keep them for appropriate tasks. Like logic heavy classes.

So, back to the library. The main intent behind is simplifying demo workflow as much as possible. Just toss your demos into folder and enjoy tree generation.

## Config

Attach VueComponentTree to your router. And yes, [vue-router](https://github.com/vuejs/vue-router) is required.
```js
import Router from 'vue-router'
import { createRoute } from 'vue-book'

const router = new Router({
  routes: [
    createRoute({
      requireContext: require.context('./..', true, /.demo.vue$/), 
      path: '/demo',
      hideFileExtensions: true, // optional, hides file extensions in list.
    }),
  ]
})
```
So, about arguments. 

`require.context('./../tree', true, /.vue$/), '/demo'`
* `./../tree` is path to your demo folder. Works the same as require/import.
* `/demo` is root route for vue-router.

Here's the vue-cli3 [demo project](https://github.com/asvae/vue-book-demo) if something doesn't work for you.

### Production

You don't have to keep demos in production. Use webpack [define-plugin](https://webpack.js.org/plugins/define-plugin/) and exclude them from bundle.

```javascript
if (process.env.NODE_ENV !== 'production') {
  const createRoute = require('vue-book').createRoute
  
  routes.push({
    path: '/demo',
    component: App,
    children: [
      createRoute({
        requireContext: require.context('./..', true, /.demo.vue$/), 
        path: '/demo',
      }),
    ],
  })
}
```

### Deploy

 * `yarn serve` - run dev server;
 * `yarn demo` - compile assets;
 * `yarn dist` - compile assets;
 * `npm publish` - publish to npm.

## Feedback | Support
Leave an issue if something doesn't work for you.

Also remember: Stars fuel package development! 

## Licence
MIT

[circleci-badge]: https://img.shields.io/circleci/project/github/asvae/vue-book/master.svg?style=flat-square
[circleci-url]: https://circleci.com/gh/asvae/vue-book 
