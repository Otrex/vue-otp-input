<template>
  <div id="app">
    <h1>OTP Input Version 1.0</h1>
    <otp-input :dimension="'30px'" />
  </div>
</template>

<script>
import OTPInput from "./components/OTPInput.vue";
export default {
  name: 'App',
  components: {
    "otp-input": OTPInput
  }
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
