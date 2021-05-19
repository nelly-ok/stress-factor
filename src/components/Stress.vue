<template>
  <div class="home">
    <h1>What is stress</h1>
    <iframe
      width="560"
      height="315"
      src="https://www.youtube.com/embed/dERu8051t4w"
      title="YouTube video player"
      frameborder="0"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen
    ></iframe>
    <button type="button" class="btn btn-success" @click="start()">
      Start
    </button>
  </div>
</template>

<script>
export default {
  name: "Stress",
  props: {
    msg: String,
  },
  methods: {
    start() {
      this.$emit("start");
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

.home {
  display: flex;
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
</style>
