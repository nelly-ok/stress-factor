<template>
  <div class="home">
    <h1>{{header}}</h1>
    <img class="stat-img" :src="img" alt="" srcset="">
    <NextButton  @prev="prev" @next="next"/>
  </div>
</template>



<script>

import NextButton from './NextButton.vue';

export default {
  name: "Stat",
  components: {
    NextButton
  },
  props: {
    msg: String,
    header: String,
    img: String
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
