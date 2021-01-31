# Vue Wavify

[![img](https://img.shields.io/npm/l/vue-wavify.svg)](https://github.com/SvenWesterlaken/vue-wavify/blob/main/LICENSE)

A single Vue component to create and adjust an animated wave using svg & javascript.

# Installation
**Yarn**

    yarn add vue-wavify

**npm**

    npm install vue-wavify


# Usage

The package can be imported globally or locally.

**Locally (single file component)**
```vue
<template>
  <div class="wave-container" fill="#f79902">
    <vue-wavify />
  </div>
</template>

<script>
import VueWavify from 'vue-wavify';

export default {
  components: { VueWavify }
});
</script>
```

**Globally**
```js
import Vue from 'vue';
import VueWavify from 'vue-wavify';

Vue.use(VueWavify);
// Or
Vue.component('vue-wavify', VueWavify);

```

# Configuration (props)


| prop        | default | type      | description |
| ----------- |:-------:|:---------:|:----------- |
| `paused`    | `false` | `Boolean` | |
| `points`    | `3`     | `Number`  | |
| `speed`     | `0.15`  | `Number`  | |
| `height`    | `20`    | `Number`  | |
| `amplitude` | `20`    | `Number`  | |
| `fill`      | `blue`  | `String`  | |

# Credits

This component/package is mainly based on the [react-wavify](https://www.npmjs.com/package/react-wavify) package and can be seen as a simple port from react to vue, implementing functionalities similar to that of [Benjamin Grauwin](http://benjamin.grauwin.me/)'s [Wavify](https://github.com/peacepostman/wavify) plug-in.
