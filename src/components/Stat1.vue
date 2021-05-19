<template>
  <div class="home">
    <h1>Next lets explore race. America (like most other countriess) has a race problem. Don’t believe? I’ll let the numbers do the talking</h1>
    <img class="stat-img" src="../assets/img/income.jpeg" alt="" srcset="">
    <NextButton  @prev="prev" @next="next"/>
  </div>
</template>



<script>

import NextButton from './NextButton.vue';

export default {
  name: "Stat1",
  components: {
    NextButton
  },
  props: {
    msg: String,
  },
  methods: {
    start() {
      this.$emit("start");
    },
    prev() {
      this.$emit("prev");
    },
    next() {
      this.$emit("next");
    },
  },
};
</script>
ß
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.navigate {
  width: 100%;
  padding: 0 2em;
  display: flex;
  justify-content: space-between;
  position: absolute;
}


</style>
