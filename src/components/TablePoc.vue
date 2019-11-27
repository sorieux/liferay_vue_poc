<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <vue-good-table
            :columns="columns"
            :rows="rows"
            :pagination-options="{
              enabled: true
            }"
            :search-options="{
              enabled: true
            }"
    />
  </div>
</template>

<script>
import 'vue-good-table/dist/vue-good-table.css'
import { VueGoodTable } from 'vue-good-table';
import axios from 'axios';


export default {
  name: 'TablePoc',
  props: {
    msg: String
  },
  components :{
    VueGoodTable
  },
  data: function() {
    return {
      columns: [
        {
          label: 'Name',
          field: 'name',
        },
        {
          label: 'Symbol',
          field: 'symbol',
        },
        {
          label: 'Price (USD)',
          field: 'price_usd',
          formatFn: this.formatPrice,
        },
        {
          label: 'Percent change 1h',
          field: 'percent_change_1h',
          formatFn: this.formatPercentage,
        },
        {
          label: 'Percent change 24h',
          field: 'percent_change_24h',
          formatFn: this.formatPercentage,
        },
        {
          label: 'Percent change 7d',
          field: 'percent_change_7d',
          formatFn: this.formatPercentage,
        },
      ],
      rows: [
      ],
    };
  },
  mounted: function() {
    axios.get('https://api.coinlore.com/api/tickers/')
            .then(response => (this.rows = response.data.data))
  },
  methods: {
    formatPercentage(value) {
      return value + '%';
    },
    formatPrice(value) {
      return value + '$';
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  @import url(http://fonts.googleapis.com/icon?family=Material+Icons);
</style>
