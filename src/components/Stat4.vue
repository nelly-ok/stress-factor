<template>
  <div class="home">
    <h1>What is stress</h1>
    <img class="stat-img" src="../assets/img/Stat4.jpg" alt="" srcset="">
    <NextButton  @prev="prev" @next="next"/>
  </div>
</template>

<script>


import NextButton from './NextButton.vue';

export default {
  name: "Stat4",
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
