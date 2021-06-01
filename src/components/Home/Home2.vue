<template>
  <div class="home-2">
    <h6>This interactive documentary explores stress and race.</h6>
    <h6>We'll explore how race and your social environment affects your health and mental wellbeing.</h6>
    <NextButton @prev="prev" @next="next" />
  </div>
</template>

<script>
import NextButton from '../NextButton'

export default {
  name: "Home2",
  props: {
    msg: String,
  },
  components: {
    NextButton
  },
  methods: {
    prev() {
      this.$emit("prev");
    },
    next() {
      this.$emit("next");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.identity-select {
  display: flex;
  width: 100%;
  padding: 0 3em;
  justify-content: space-between;
}

.home-2 {
  display: flex;
  padding: 4em 9em;
  flex-direction: column;
  align-items: center;
  height: 80vh;
  justify-content: unset !important;
}

.select-third {
  width: 25%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.stat-img {
  width: 55%;
}
</style>
