<template>
  <div class="home-1">
    <h1>Welcome to Stress Factor</h1>
    <NextButton :hideLeft="true"  @prev="prev" @next="next" />
  </div>
</template>

<script>

import NextButton from '../NextButton'
export default {
  name: "Home1",
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

.home-1 {
  display: flex;
      padding: 4em;
  flex-direction: column;
  align-items: center;
  height: 100vh;
  justify-content: space-around;
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
