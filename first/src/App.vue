<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" :date="currentDate" />
    <Calculator />
    <button v-on:click="onClick">Click me</button> / {{ count }}
    <button @click="count = 1 + 2">Sum</button>

    {{ massage }}
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import Calculator from "./components/Calculator.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    Calculator,
  },
  data() {
    return {
      count: 0,
      currentDate: new Date().toDateString(),
      massage: "Hello Vue",
    };
  },
  methods: {
    onClick() {
      this.count += 1;
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
