<template>
  <div>
    <mdc-button @click="hello">
      Click me!
    </mdc-button>

    <mdc-progress :progress="progress"></mdc-progress>
  </div>
</template>

<script>
  import MdcButton from './MdcButton.vue'
  import MdcProgress from './MdcProgress.vue'

  export default {
    components: {MdcButton, MdcProgress},

    data() {
      return {
        progress: 0
      }
    },

    mounted() {
      setInterval(() => {
        this.progress = (this.progress + 10) % 100
      }, 500)
    },

    methods: {
      hello() {
        console.log('Hello, world!')
      }
    }
  }
</script>
