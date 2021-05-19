<template>
  <div class="home">
    <h1>Welcome to Stress Factor</h1>
    <div class="identity-select">
      <div class="select-third">
        <h6>Gender:</h6>
        <select class="form-select" aria-label="Default select example">
          <option selected>Open this select menu</option>
          <option value="1">One</option>
          <option value="2">Two</option>
          <option value="3">Three</option>
        </select>
      </div>
      <div class="select-third">
        <h6>Age:</h6>
        <select class="form-select" aria-label="Default select example">
          <option selected>Open this select menu</option>
          <option value="1">One</option>
          <option value="2">Two</option>
          <option value="3">Three</option>
        </select>
      </div>
      <div class="select-third">
        <h6>Sexual Orientation:</h6>
        <select class="form-select" aria-label="Default select example">
          <option selected>Open this select menu</option>
          <option value="1">One</option>
          <option value="2">Two</option>
          <option value="3">Three</option>
        </select>
      </div>
    </div>
    <button type="button" class="btn btn-success" @click="start()">
      Start
    </button>
  </div>
</template>

<script>
export default {
  name: "Home",
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
<style >
.identity-select {
  display: flex;
  width: 100%;
  padding: 0 3em;
  justify-content: space-between;
}

.home {
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
  width: 75%;
}
</style>
