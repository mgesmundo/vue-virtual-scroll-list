<a href="https://npmjs.com/package/vue-virtual-scroll-list">
    <img src="https://img.shields.io/npm/v/vue-virtual-scroll-list.svg?style=flat" alt="NPM version"/>
</a>
<a href="https://npmjs.com/package/vue-virtual-scroll-list">
    <img src="https://img.shields.io/npm/dm/vue-virtual-scroll-list.svg">
</a>
<a href="http://packagequality.com/#?package=vue-virtual-scroll-list">
    <img src="http://npm.packagequality.com/shield/vue-virtual-scroll-list.svg">
</a>
<a href="https://vuejs.org/">
    <img src="https://img.shields.io/badge/vue-2.x-brightgreen.svg" alt="Vue version"/>
</a>
<a href="https://github.com/tangbc/vue-virtual-scroll-list/blob/master/LICENSE">
    <img src="https://img.shields.io/github/license/tangbc/vue-virtual-scroll-list.svg" alt="MIT License"/>
</a>


## vue-virtual-scroll-list

> A vue (2.x) component that supports big data and infinite loading by using virtual scroll list.

* Tiny and very very easy to use.

* Big data list with high performance.

* Support fixed height and variable height.

* Support set the initial scroll index or change any.

* Event scrolling, reach top and bottom can be detected.


## Live demos

* [vue-virtual-scroll-list with 100,000 finite data](https://tangbc.github.io/vue-virtual-scroll-list/examples/finite/).

* [vue-virtual-scroll-list with requesting infinite data](https://tangbc.github.io/vue-virtual-scroll-list/examples/infinite/).

* [vue-virtual-scroll-list with variable height](https://tangbc.github.io/vue-virtual-scroll-list/examples/variable/).


## How it works

<img src="https://tangbc.github.io/github-images/virtual-scroll-list-2.gif">


## Simple usage

#### Using by npm:

```
npm install vue-virtual-scroll-list --save
```

```vue
<template>
    <div>
        <virtualList :size="40" :remain="8">
            <Item v-for="(item, index) of items" :item="item" :key="item.id" />
        </virtualList>
    </div>
</template>

<script>
    import Item from '../item.vue'
    import virtualList from 'vue-virtual-scroll-list'

    export default {
        name: 'demo',
        data () {
            return {
                items: [...]
            }
        },
        components: { Item, virtualList }
    }
</script>
```

The `<Item>` component is included inside but defined outside the `<virtualList>` component, we see that `<virtualList>` does **not** rely on the `<Item>` component, so you can use virtual-list with any component freely.

#### Using by script include:

```html
<script src="https://unpkg.com/vue@2.0.0/dist/vue.js"></script>
<script src="https://tangbc.github.io/vue-virtual-scroll-list/index.js"></script>

<div id="app">
    <virtual-list :size="40" :remain="8" wtag="ul">
        <li class="item" v-for="(udf, index) of items" :key="index">Item: # {{ index }}</li>
    </virtual-list>
</div>
```

```javascript
// Global name as `VirtualScrollList`
Vue.component('virtual-list', VirtualScrollList)

new Vue({
    el: '#app',
    data: {
        items: new Array(100000)
    }
})
```


## Notice

* List `<Item/>` component or DOM frag using `v-for` must designate the `:key` property.

* Consider use `box-sizing: border-box;` on `<Item/>` if you want absolutely correct scroll height.


## Props type

<img height="256" src="https://tangbc.github.io/github-images/vitual-scroll-list-4.png">

*Prop* | *Type* | *Required* | *Description* |
:--- | :--- | :--- | :--- |
| size | Number | ✓ | Each list item height, in variable height mode, this prop just use to calculate the virtual-list viewport height. |
| remain | Number | ✓ | How many items should be shown in virtual-list viewport, so `size` and `remain` determine the outside container viewport height (size × remian). |
| start | Number | * | Default value is `0`, the initial scroll start index. It must be integer and in the range of list index, if out of range it will be turned to `0` or the last one.  |
| bench | Number | * | Default value is equal to `remain`, unreached items count, not show in virtual-list viewport but exist in real DOM, the larger the bench, the higher the scroll performance will achieved.  |
| debounce | Number | * | **It's disabled by default**, milliseconds of using `debounce` function to ensure scroll event doesn't fire so often that it bricks browser performance. |
| rtag | String | * | Default value is `div`, the virtual-list root element tag name, in all cases it's style is set to `display: block;` |
| wtag | String | * | Default value is `div`, the virtual-list item wrapper element tag name, in all cases it's style is set to `display: block;` |
| wclass | String | * | Default value is an empty string, the virtual-list item wrapper element class, has the same API with [`v-bind:class`](https://vuejs.org/v2/guide/class-and-style.html) |
| totop | Function | * | Called when virtual-list is scrolled to top, no param. |
| tobottom | Function | * | Called when virtual-list is scrolled to bottom, no param. |
| onscroll | Function | * | Called when virtual-list is scrolling, param: `(e, { offset, offsetAll, start, end })`. |
| variable | Function or Boolean | * | For using virtual-list with variable height mode. If assign `Function`, this prop is a variable height getter function which is called with param: `(index)` when each item is ready to be calculated. If assign `Boolean`, virtual-list will get each item variable height by it's inline style height automatic. |

### About variable height

In variable height mode, prop `size` is still required. All the index variable height and scroll offset will be cached by virtual-list after the binary-search calculate, if you want to change anyone `<Item/>` height from data, you should call virtual-list's `updateVariable(index)` method to clear the offset cached, refer to [variable example](https://github.com/tangbc/vue-virtual-scroll-list/blob/master/examples/variable/variable.vue#L1) source for detail.

If you are using `variable` assign by `Boolean`, **do not** set inline style height inside `<item/>` component, you must set inline style height on `<item/>` component outside directly, such as:
```vue
<template>
    <div>
        <virtualList :size="40" :remain="8" :variable="true">
            <Item v-for="item of items" :key="item.id" :style="{ height: item.height + 'px' }" />
        </virtualList>
    </div>
</template>
```


## Contributions

Welcome to improve vue-virtual-scroll-list with any issue, pull request or code review.


## Changelogs

Maintain and update occasionally, for changes see [release](https://github.com/tangbc/vue-virtual-scroll-list/releases).

## License

[MIT License](https://github.com/tangbc/vue-virtual-scroll-list/blob/master/LICENSE)
