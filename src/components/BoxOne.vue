<template>
  <div>
    <b-container class="box">
      <p>
        <span
          class="title"
        >The EuroJackpot numbers for {{addCero(contentBoxOne.date.day)}}.{{addCero(contentBoxOne.date.month)}}.{{contentBoxOne.date.year}}</span>
      </p>
      <p>The {{contentBoxOne.nr}}th draw for the EuroJackpot was held on {{addCero(contentBoxOne.date.day)}}.{{addCero(contentBoxOne.date.month)}}.{{contentBoxOne.date.year}}, as usual at 9pm in Helsinki..</p>
    </b-container>
  </div>
</template>

<script>
export default {
  props: {
    contentBoxOne: Object
  },
  methods: {
    addCero(str) {
      str = str.toString();
      if (str.length < 2) {
        str = "0" + str;
      }
      return str;
    }
  }
};
</script>


<style scoped>
.box {
  border: 1px solid #d9deda;
  border-left: none;
  box-shadow: -7px 0 0 0 #69a507;
  margin-bottom: 14px;
  margin-left: 7px;
  padding: 14px;
}
.title {
  font-size: 16px;
}
p {
  text-align: left;
}
</style>
</style>