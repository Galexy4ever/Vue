<template>
  <div>
    <button v-on:click="visible = !visible" class="addBut">
      ADD NEW COST+
    </button>
    <div v-show="visible" class="payment-form">
      <input placeholder="Date" type="text" v-model.trim="date" />

      <input placeholder="Category" type="text" v-model.trim="category" />
      <input placeholder="Amout" type="number" v-model.number="value" />
      <button @click="onClick">Save</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddPaymentForm",
  data() {
    return {
      value: 0,
      category: "",
      date: "",
      visible: false,
    };
  },
  methods: {
    getCurrentDate() {
      const today = new Date();
      const d = today.getDate();
      const m = today.getMonth() + 1;
      const y = today.getFullYear();
      return `${d}.${m}.${y}`;
    },
    onClick() {
      console.log("Saved");
      const { value, category } = this;
      const data = {
        date: this.date || this.getCurrentDate(),
        category,
        value,
      };
      this.$emit("addNewPayment", data);
    },
  },
};
</script>

<style>
.addBut {
  padding: 20px;
  color: rgb(39, 2, 8);
  border-radius: 10px 100px / 120px;
  margin-bottom: 30px;
  background: rgb(155, 14, 155);
}
</style>