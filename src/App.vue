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
      <b-row>
        <b-col cols="9">
          <CenterTable :table="table"></CenterTable>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import axios from "axios"; // For the api-rest query
import Numbers from "./components/Numbers"; //component to show winning numbers
import CenterTable from "./components/CenterTable"; // Central table width data

export default {
  name: "App",
  components: {
    Numbers,
    CenterTable
  },
  data() {
    return {
      numbers: [],
      date: {},
      tableContent: {},
      table: []
    };
  },
  mounted() {
    axios
      .get("https://www.lottoland.com/api/drawings/euroJackpot")
      .then(response => {
        this.numbers = response.data.last.numbers.concat(
          response.data.last.euroNumbers
        );
        this.tableContent = response.data.last.odds;
        this.date = response.data.last.date;

        for (let i in this.tableContent) {
          this.tableContent[i].prize = this.tableContent[i].prize;
          this.tableContent[i].winners = this.tableContent[i].winners;
          this.table.push(this.tableContent[i]);
        }
      })
      .catch(error => {
        console.log(error);
      })
      .finally(() => (this.loading = false));
  }
};
</script>
