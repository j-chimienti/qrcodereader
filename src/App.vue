<template>
  <div>
    <div class="container">
      <h1>QR Code Reader</h1>
      <small v-if="error" class="text-red">{{error}}</small>
      <h2>Stream</h2>
      <h3 v-if="text">{{text}}</h3>
      <div class="row justify-content-center">
        <QrcodeStream @decode="onDecoded" @init="onInit" style="max-width: 600px"/>
      </div>
    
    </div>
    <p class="text-center"><a :href="github">{{github}}</a></p>
  </div>
</template>

<script>
import {QrcodeStream} from 'vue-qrcode-reader' 

const github = "https://github.com/j-chimienti/qrcodereader"

export default {
  name: 'App',
  data() { return { text: "", error: null, github}},
  methods: {
    onDecoded(e) {
      this.text = e
    },
     async onInit (promise) {
      try {
        await promise
      } catch (error) {
        if (error.name === 'NotAllowedError') {
          this.error = "ERROR: you need to grant camera access permission"
        } else if (error.name === 'NotFoundError') {
          this.error = "ERROR: no camera on this device"
        } else if (error.name === 'NotSupportedError') {
          this.error = "ERROR: secure context required (HTTPS, localhost)"
        } else if (error.name === 'NotReadableError') {
          this.error = "ERROR: is the camera already in use?"
        } else if (error.name === 'OverconstrainedError') {
          this.error = "ERROR: installed cameras are not suitable"
        } else if (error.name === 'StreamApiNotSupportedError') {
          this.error = "ERROR: Stream API is not supported in this browser"
        } else if (error.name === 'InsecureContextError') {
          this.error = 'ERROR: Camera access is only permitted in secure context. Use HTTPS or localhost rather than HTTP.';
        } else {
          this.error = `ERROR: Camera error (${error.name})`;
        }
      }
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

.text-red {
  color: red;
}
</style>
