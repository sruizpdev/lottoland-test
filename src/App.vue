<template>
  <div id="app">
    <b-container>
      <b-row>
        <div class="banner">
          <h2>EUROJACKPOT RESULTS & WINNING NUMBERS</h2>
        </div>
      </b-row>
      <b-row>
        <Numbers :numbers="numbers" :date="date"></Numbers>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import axios from "axios"; // For the api-rest query
import Numbers from './components/Numbers' //component to show winning numbers

export default {
  name: 'App',
  components: {
    Numbers
  },
  data() {
    return {
      numbers: [],
      date: {}
    };
  },
  mounted() {
    axios
      .get("https://www.lottoland.com/api/drawings/euroJackpot")
      .then(response => {
        this.numbers = response.data.last.numbers.concat(
          response.data.last.euroNumbers
        );
        this.date = response.data.last.date;
      })
      .catch(error => {
        console.log(error);
      })
      .finally(() => (this.loading = false));
  }
}
</script>
