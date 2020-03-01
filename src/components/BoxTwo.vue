<template>
  <div>
    <b-container class="box">
      <p>
        <span
          class="title"
        >EuroJackpot numbers for {{addCero(contentBoxTwo.day)}}.{{addCero(contentBoxTwo.month)}}.{{contentBoxTwo.year}}</span>
      </p>
      <p>The balls used for the draw are made of a synthetic polymer, softer than ping-pong balls. The results are broadcast after the draw, with the draw-machines independently checked by the VTT Technical Research Center of Finland.</p>
      <p>Lottoland published the draw results immediately after the draw on {{addCero(contentBoxTwo.day)}}.{{addCero(contentBoxTwo.month)}}.{{contentBoxTwo.year}}.</p>
    </b-container>
  </div>
</template>

<script>
export default {
  props: {
    contentBoxTwo: Object
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