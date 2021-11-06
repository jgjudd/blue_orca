<template>
  <div id="container">
    <h3>{{ inflationData.name }}</h3>
    <table>
      <tr>
        <th>Date</th>
        <th>Value</th>
      </tr>
      <tr v-for="row in inflationData.data" v-bind:key="row.date">
        <td>{{ row.date }}</td>
        <td>{{ row.value }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: 'Table-Inflation',
  data() {
    return {
      inflationData: []
    }
  },
  async created() {
      await fetch("https://www.alphavantage.co/query?function=INFLATION&apikey=16RM7YB3WU85H52Z")
      .then(res => res.json())
      .then(json => this.inflationData = json);
  }
}
</script>

<style>

table, th, td {
  border: 1px solid black;
  border-collapse: collapse;
  padding: 6px;
  margin: auto;
}
</style>
