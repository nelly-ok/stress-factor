<template>
  <div class="home">
    <h1>Education analysis</h1>
    <img class="stat-img" src="../assets/img/education-pays.jpg" alt="" srcset="">
    <h3>Lets do some multiplication</h3>
    <h3>Yearly:</h3>
    <vue-bar-graph
      :points="[{label: '< High School', value: 32188}, {label: 'High School', value: 40612}, {label: 'Some college', value: 45604}, {label: 'Associates', value: 48776}, {label: 'Bachelors', value: 67860}, {label: 'Masters', value: 80340}, {label: 'Professional', value: 98436}, {label: 'Doctoral', value: 98020}]"
      :show-y-axis="true"
      :show-x-axis="true"
      :width="600"
      :height="200"
      :show-values="true"
      :show-trend-line="true"
      :trend-line-width="2"
      trend-line-color="lightblue"
    />
    <p></p>
    <img class="stat-img" src="../assets/img/sat.jpg" alt="" srcset="">
    <NextButton  @prev="prev" @next="next"/>
  </div>
</template>



<script>

import NextButton from './NextButton.vue';
import VueBarGraph from 'vue-bar-graph';

export default {
  name: "EducationAnalysis",
  components: {
    NextButton,
    VueBarGraph,
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

.home {
  height: unset;
}
</style>
