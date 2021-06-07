<template>
  <div class="home">
    <h1>Choose an Identity</h1>
    <div class="identity-select">
      <div class="select-third">
        <h4>Gender:</h4>
        <select v-model="demo.gender" class="form-select" aria-label="Default select example">
          <option value="woman" selected>Woman</option>
          <option value="man">Man</option>
          <option value="trans">Trans</option>
          <option value="enby">Non-binary</option>
          <option value="queer">Queer/Non-conforming</option>
          <option value="no">Prefer not to answer</option>
        </select>
        
      </div>
      <div class="select-third">
        <h4>Age:</h4>
        <select v-model="demo.age" class="form-select" aria-label="Default select example">
          <option selected>5-10</option>
          <option value="1">10-18</option>
          <option value="2">18-30</option>
          <option value="3">30+</option>
          <option value="4">Prefer not to answer</option>
        </select>
      </div>
      <div class="select-third">
        <h4>Sexual Orientation:</h4>
        <select v-model="demo.sex" class="form-select" aria-label="Default select example">
          <option selected>Straight</option>
          <option value="1">Gay/Lesbian</option>
          <option value="2">Bi-sexual</option>
          <option value="3">Queer</option>
          <option value="4">Prefer not to answer</option>
        </select>
      </div>
    </div>
    <button type="button" class="btn btn-success" @click="start()">
      Start
    </button>
    <NextButton :hideRight="true"  @prev="prev"  />
  </div>
</template>

<script>

import NextButton from '../NextButton'

export default {
  name: "Home3Start",
  props: {
    msg: String,
  },
  methods: {
    start() {
      this.$emit("start", this.demo);
    },
    prev() {
      this.$emit("prev");
    },
  },
  components: {
    NextButton
  },
  data() {
    return {
      demo: {
        gender: "woman",
        age: "5-10",
        sex: "Straight",
      }
    }
  }
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
      padding: 4em;
  flex-direction: column;
  align-items: center;
  height: 80vh;
  justify-content: space-around;
}

.select-third {
  width: 25%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.stat-img {
  width: 50%;
}
</style>
