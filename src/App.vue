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
  methods: {
    comas(str) {
      str = str.toString();
      switch (str.length) {
        case 10:
          str =
            str.slice(0, 2) +
            "," +
            str.slice(2, 5) +
            "." +
            str.slice(5, 8) +
            "." +
            str.slice(8, 10);
          break;
        case 9:
          str =
            str.slice(0, 1) +
            "," +
            str.slice(1, 4) +
            "." +
            str.slice(4, 7) +
            "." +
            str.slice(7, 9);
          break;
        case 8:
          str = str.slice(0, 3) + "," + str.slice(3, 6) + "." + str.slice(6, 8);
          break;
        case 7:
          str = str.slice(0, 2) + "," + str.slice(2, 5) + "." + str.slice(5, 7);
          break;
        case 6:
          str = str.slice(0, 1) + "," + str.slice(1, 4) + "." + str.slice(4, 6);
          break;
        case 5:
          str = str.slice(0, 3) + "," + str.slice(3, 5);
          break;
        case 4:
          str = str.slice(0, 2) + "," + str.slice(2, 4);
          break;
        case 3:
          str = str.slice(0, 1) + "," + str.slice(1, 3);
          break;
      }
      return str;
    }
      
  
    
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
          this.tableContent[i].orden =  this.tableContent[i].prize;
          this.tableContent[i].prize = this.comas(this.tableContent[i].prize);
          this.tableContent[i].winners = this.comas(
            this.tableContent[i].winners
          );
          this.table.push(this.tableContent[i]);
        }
        
        
        this.table.shift();
        this.table.sort((a, b) => b.orden - a.orden);
      })
      .catch(error => {
        console.log(error);
      })
      .finally(() => (this.loading = false));
  }
};
</script>
