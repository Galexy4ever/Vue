<template>
  <div>
    <div class="logs" v-for="(log, id) in logs" :key="id">
      {{ log }}
    </div>

    <input
      type="number"
      v-model.lazy="operand1"
      placeholder="operand1"
      v-bind:disabled="check !== 1"
    />
    <input
      type="number"
      v-model.lazy="operand2"
      placeholder="operand2"
      v-bind:disabled="check !== 2"
    />
    <div>= {{ result }}</div>
    <div>= fib {{ fibResult }}</div>

    <div class="error" :class="{ red: error }" v-if="error">
      Ошибка!! {{ error }}
    </div>

    <div class="error" :class="{ red: error }" v-show="!!error">
      Ошибка!! {{ error }}
    </div>

    <div class="strange-message">
      <template v-if="result < 0"> Получилось отрицательное число </template>
      <template v-else-if="result < 100"
        >Получилось число в первой сотне</template
      >
      <template v-else>Все остальные числа</template>
    </div>

    <div class="keyboard">
      <button
        class=""
        v-for="operand in operands"
        @click="calculate(operand)"
        :key="operand"
        v-bind:title="operand"
      >
        {{ operand }}
      </button>
    </div>
    <input type="checkbox" v-on:click="visible = !visible" />
    <label for="checkbox">Включить экранную клавиатуру</label><br />
    <div v-show="visible" class="numbers">
      <button
        class=""
        v-for="number in myNumbers"
        @click="getOper(number)"
        :key="number"
        v-bind:title="number"
      >
        {{ number }}
      </button>

      <button @click="del()">Delete</button>
    </div>
    <div>
      <input name="inputBut" type="radio" :onchange.prop="getOper1" />Операнд 1
      <input name="inputBut" type="radio" :onchange.prop="getOper2" />Операнд 2
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      myNumbers: ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0"],
      operands: ["+", "-", "/", "*"],
      check: "",
      checked: "",
      text1: "",
      operand1: "",
      operand2: "",
      fibResult: 0,
      result: 0,
      error: "",
      logs: {},
      visible: false,
    };
  },

  methods: {
    calculate(operation = "+") {
      this.error = "";
      switch (operation) {
        case "+":
          this.add();
          break;
        case "-":
          this.substract();
          break;
        case "*":
          this.multiply();
          break;
        case "/":
          this.divide();
          break;
      }
      const key = Date.now();
      const value = `${this.operand1}${operation}${this.operand2} = ${this.result}`;
      this.$set(this.logs, key, value);
    },
    del() {
      if (this.check == 1) {
        this.operand1 = this.operand1.slice(0, -1);
      } else {
        this.operand2 = this.operand2.slice(0, -1);
      }
    },
    getOper(num) {
      if (this.check == 1) {
        this.operand1 = this.operand1 + num;
      } else {
        this.operand2 = this.operand2 + num;
      }
    },
    getOper1() {
      this.check = 1;
    },
    getOper2() {
      this.check = 2;
    },
    add() {
      this.result = +this.operand1 + +this.operand2;
      this.fibResult = this.fib1 + this.fib2;
    },
    substract() {
      console.log("substract");
      this.result = +this.operand1 - +this.operand2;
    },
    multiply() {
      this.result = +this.operand1 * +this.operand2;
    },
    divide() {
      const { operand1, operand2 } = this;

      if (+operand2 === 0) {
        return (this.error = "Делить на 0 нельзя");
      }

      this.result = +operand1 / +operand2;
    },
    sendData(data) {
      console.log("Send Data name", data);
    },
    fib(n) {
      return n <= 1 ? n : this.fib(n - 1) + this.fib(n - 2);
    },
  },
  computed: {
    fib1() {
      return this.fib(this.operand1);
    },
    fib2() {
      return this.fib(this.operand2);
    },
  },
};
</script>
<style scoped>
.red {
  color: red;
}
</style>