# vue-mdc

> Example of how to use material-components-web (mdc) in Vue

This is an example project to show how to include and use 
[material-components-web](https://github.com/material-components/material-components-web) (mdc)
in a Vue (using webpack) project.  
This is not a wrapper project, or adapter, instead it's a demo of how to 
add the mdc library directly. This can be be nice if a wrapper isn't sufficient or 
does not work as expected.  
If you are looking for a wrapper, then take a look at [posva/vue-mdc](https://github.com/posva/vue-mdc) or [stasson/vue-mdc-adapter](https://github.com/stasson/vue-mdc-adapter).

## Install

The starting point of this project is `vue-cli` using the `webpack-simple` template.

``` bash
npm i vue-cli
./node_modules/.bin/vue init webpack-simple
? Use sass? Yes

npm i

# Then install mdc
npm i material-components-web
```

## Configuration

Now it's possible to import components in your SFC files, 
e.g., `import {MDCLinearProgress} from '@material/linear-progress'`.  
But the css is a bit tricky;  
components in mdc refer to other components inside the `@material`
folder in `node_modules`, so webpack configuration must be set up
so mdc components can resolve the internal components.  
There seems to be several ways to do this, the solution I use is

``` JavaScript
scss: 'vue-style-loader!css-loader!sass-loader?' + JSON.stringify({
  includePaths: ['node_modules']
})
```

This way all the loaders are loaded, and `node_modules` is added to include path.

## Code

Here is an example of how to use the [button](https://material.io/components/web/catalog/buttons)

``` html
<template>
  <button class="mdc-button" @click="$emit('click')">
    <slot></slot>
  </button>
</template>

<style lang="scss">
  @import '@material/button/mdc-button';
</style>
```

If you want to include [ripple effect](https://material.io/components/web/catalog/ripples)
you need to import `MDCRipple`, and remember to destroy it on component destroy.

``` html
<template>
  <button ref="button" class="mdc-button" @click="$emit('click')">
    <slot></slot>
  </button>
</template>

<script>
  import {MDCRipple} from '@material/ripple'

  export default {
    mounted() {
      this.ripple = new MDCRipple(this.$refs.button)
    },

    destroyed() {
      this.ripple.destroy()
    }
  }
</script>

<style lang="scss">
  @import '@material/button/mdc-button';
</style>
```

This code should be the same as in [MdcButton.vue](src/MdcButton.vue).

## License

MIT © Eirik Brandtzæg
