<template>
    <div id="search-wrapper">
        <div>
          <input type="text" v-on:input="e => symbolSearch(e.target.value)" placeholder="Symbol Search..." style="width:100%;" />
          <p v-for="result in searchResults" v-bind:key="result.symbol">({{ result['1. symbol'] }}) {{ result['2. name'] }}</p>
        </div>
    </div>
</template>

<script>
export default {
  name: 'SymbolSearch',
  data () {
    return {
      searchResults: []
    }
  },
  methods: {
    async symbolSearch (searchTerm) {
      if (searchTerm.length === 0 || searchTerm === undefined) {
        console.log('Reset this.searchResults')
        this.searchResults = []
      } else {
        const results = await fetch(`https://www.alphavantage.co/query?function=SYMBOL_SEARCH&keywords=${searchTerm}&apikey=16RM7YB3WU85H52Z`)
          .then(res => res.json())
        console.log(results.bestMatches)
        this.searchResults = results.bestMatches || [{ '1. symbol': '-', '2. name': 'No Results To Display' }]
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#search-wrapper {
  text-align: left;
}
</style>
