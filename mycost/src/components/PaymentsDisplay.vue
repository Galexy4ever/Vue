<template>
  <div class="list">
    <table class="table">
      <tr>
        <td class="tableHead">#</td>
        <td class="tableHead">Date</td>
        <td class="tableHead">Category</td>
        <td class="tableHead">Cost</td>
      </tr>
    </table>
    <hr />
    <table class="item" v-for="(item, idx) in items" v-bind:key="idx">
      <tr>
        <td class="td">{{ idx + 1 }}</td>
        <td class="td">{{ item.date }}</td>
        <td class="td">{{ item.category }}</td>
        <td class="td">{{ item.value }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "PaymentsDisplay",
  props: {
    items: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style>
.tableHead {
  height: 50px;
  width: 200px;
  padding: 15px;
  text-align: center;
  color: gray;
  font-size: 30px;
}

.td {
  height: 50px;
  width: 200px;
  padding: 15px;
  text-align: center;
  color: black;
  font-size: 25px;
}
</style>