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
