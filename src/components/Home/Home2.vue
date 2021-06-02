<template>
  <div class="home-2">
    <h3>This interactive documentary explores stress and race.</h3>
    <h3>We'll explore how race and your social environment affects your health and mental wellbeing.</h3>
    <h3>The focus of this thought experiment will be Black Americans. I understand that race/racism doesn't exist in a Black/White binary, I'll make references to other races wherever relevant. I'm a Black American so thats the area I'm most passionate about and chose to focus on. </h3>
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
  text-align: center;
  height: 100vh;
  justify-content: center;
}

.select-third {
  width: 25%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.stat-img {
  width: 65%;
}
</style>
