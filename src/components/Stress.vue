<template>
  <div class="home">
    <h3>What is stress</h3>
    <iframe
      width="560"
      height="315"
      src="https://www.youtube.com/embed/dERu8051t4w"
      title="YouTube video player"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen
    ></iframe>
    <NextButton @prev="prev" @next="next" />
  </div>
</template>

<script>

import NextButton from './NextButton'

export default {
  
  name: "Stress",
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
