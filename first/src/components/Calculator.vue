<template>
  <div>
    <input type="number" v-model.number="number1" placeholder="number1" />

    <div class="keyboard">
      <button v-on:click="sum = number1 + number2">+</button>
      <button v-on:click="sum = number1 - number2">-</button>
      <button @click="mult">*</button>
      <button @click="foo(number1, number2)">/</button>
      <button @click="level(number1, number2)">в степени</button>
      <button @click="level2(number1, number2)">Ц/Ч деление</button>
    </div>

    <input type="number" v-model.number="number2" placeholder="number2" />
    <br />
    равно
    <h3>{{ sum }}</h3>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      number1: 0,
      number2: 0,
      sum: 0,
    };
  },
  methods: {
    mult() {
      this.sum = this.number1 * this.number2;
    },
    foo(number1, number2) {
      this.sum = number1 / number2;
    },
    level(num1, num2) {
      this.sum = num1 ** num2;
    },
    level2(number1, number2) {
      if (number2 != 0) {
        this.sum = parseInt(this.number1 / this.number2);

        console.log(this.sum);
      } else {
        this.sum = "Error";
      }
    },
  },
};
</script>

<style>
</style>