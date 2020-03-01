<template>
  <div class="principal">
    <table class="table">
      <thead>
        <tr>
          <th>Tier</th>
          <th>Match</th>
          <th>Winners</th>
          <th>Amount</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in table" :key="item" class="linea">
          <td class="tier">{{getRomanNumber(index)}}</td>
          <td class="match">{{getText(index)}}</td>
          <td class="winners">{{item.winners}}x</td>
          <td class="amount">€ {{item.prize}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    tableContent: Object,
    table: []
  },

  methods: {
      // Get roman number
    getRomanNumber(index) {
      let romansNumbers = [
        "I",
        "II",
        "III",
        "IV",
        "V",
        "VI",
        "VII",
        "VIII",
        "IX",
        "X",
        "XI",
        "XII"
      ];
      return romansNumbers[index];
    },
    // Text for the first column
    getText(index) {
      let text = [
        "5 Numbers + 2 Euronumbers",
        "5 Numbers + 1 Euronumber",
        "5 Numbers + 0 Euronumbers",
        "4 Numbers + 2 Euronumbers",
        "4 Numbers + 1 Euronumber",
        "4 Numbers + 0 Euronumber",
        "3 Numbers + 2 Euronumbers",
        "2 Numbers + 2 Euronumbers",
        "3 Numbers + 1 Euronumber",
        "3 Numbers + 0 Euronumbers",
        "1 Number + 2 Euronumbers",
        "2 Numbers + 1 Euronumber"
      ];
      return text[index];
    }
  }
};
</script>
<style scoped>
.table {
  text-align: left;
 
  border: 1px #d8d8d8 solid;
  border-spacing: 0px;
}
td {
  padding: 10px 0px 10px 0px;
}
td {
  border-bottom: 1px #d8d8d8 solid;
}
.tier {
  width: 10%;
  padding: 14px;
}
</style>