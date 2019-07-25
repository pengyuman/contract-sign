<template>
  <div id='home'
       @click='toadt'>

  </div>
</template>

<script>
import { Popup } from 'mint-ui'

export default {
  name: 'Home',
  component: (Popup.name, Popup),
  data () {
    return {
      msg: '这是一个demo'
    }
  },
  methods: {
    toadt () {

    }
  }
}
</script>
<style>
</style>
