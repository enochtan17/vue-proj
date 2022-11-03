<template>
  <button
    @click="onClick()"
  >
    {{ text }}
  </button>
</template>

<script>
  export default {
    name: 'Button',
    props: {
      text: {
        type: String,
        default: ''
      },
      color: {
        type: String,
        default: 'blue'
      }
    },
    methods: {
      onClick() {
        console.log('click')
      }
    }
  }
</script>
