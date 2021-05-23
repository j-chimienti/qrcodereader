<template>
  <div id="app">
    <h3>{{text}}</h3>
    <QrcodeStream @decode="onDecoded" style="height: 50vh; max-height: 500px"/>
  </div>
</template>

<script>
import {QrcodeStream} from 'vue-qrcode-reader'

export default {
  name: 'App',
  data() { return { text: ""}},
  methods: {
    onDecoded(e) {
      this.text = e
    }
  },
  components: {QrcodeStream}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
