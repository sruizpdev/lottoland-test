<template>
  <div>
    <b-container>
      <b-row>
        <p>EuroJackpot Results for {{getWeekDay()}} {{date.day}} {{addCero(date.month)}} {{date.year}}</p>
      </b-row>

      <b-row>
        <ul>
          <li
            v-for="(number, index) in numbers"
            :key="index"
            class="lotery-number"
            :class="{'lotery-number-border' : index >= 5 }"
          >{{number}}</li>
        </ul>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "Numbers",
  props: {
    numbers: Array, 
    date: {} 
  },
  methods: {
    // Add extra digit to a two character string
    addCero(str) {
      str = str.toString();
      if (str.length < 2) {
        str = "0" + str;
      }
      return str;
    },
    // To get the day of the week
    getWeekDay() {
      let d = new Date();
      let weekDays = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday"
      ];
      return weekDays[d.getDay()];
    }
  }
};
</script>


<style scoped>
.lotery-number,
.lotery-number-border {
  display: inline;
  border-radius: 50%;
  display: inline-block;
  font-size: 17px;
  line-height: 35px;
  text-align: center;
  border: 1px solid #d9deda;
  border-radius: 50%;
  margin-right: 7px;
  margin-bottom: 7px;
  width: 35px;
  height: 35px;
}
/* Changing color for the last two numbers */
.lotery-number-border {
  border: 1px solid #a35a15;
}

p {
  margin-left: 17px;
  font-size: 18px;
}
</style>