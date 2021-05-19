<template>
  <section>
    <label id="minutes">00</label>:<label id="seconds">00</label>
    <Home v-if="home" @start="start" msg="Welcome to Your Vue.js App" />
    <Stress v-if="comp[0]" @prev="prev(0)" @next="next(0)" />
    <Stat1 v-if="comp[1]" @prev="prev(1)" @next="next(1)" />
    <Stat2 v-if="comp[2]" @prev="prev(2)" @next="next(2)" />
    <Stat3 v-if="comp[3]" @prev="prev(3)" @next="next(3)" />
    <Stat4 v-if="comp[4]" @prev="prev(4)" @next="next(4)" />
    <Stat5 v-if="comp[5]" @prev="prev(5)" @next="next(5)" />
  </section>
</template>

<script>
import Home from "./components/Home.vue";
import Stress from "./components/Stress.vue";
import Stat1 from "./components/Stat1.vue";
import Stat2 from "./components/Stat2.vue";
import Stat3 from "./components/Stat3.vue";
import Stat4 from "./components/Stat4.vue";
import Stat5 from "./components/Stat5.vue";

export default {
  name: "App",
  components: {
    Home,
    Stress,
    Stat1,
    Stat2,
    Stat3,
    Stat4,
    Stat5,
  },
  data() {
    return {
      home: true,
      stress: false,
      comp0: false,
      comp1: false,
      comp: { 0: false, 1: false, 2: false, 3: false, 4: false, 5: false },
      minutesLabel: false,
      secondsLabel: false,
      totalSeconds: 0,
    };
  },
  mounted() {
    //https://stackoverflow.com/questions/5517597/plain-count-up-timer-in-javascript
    this.minutesLabel = document.getElementById("minutes");
    this.secondsLabel = document.getElementById("seconds");
    setInterval(this.setTime, 1000);
  },
  methods: {
    start() {
      console.log("start");
      this.home = false;
      this.comp[0] = true;
    },
    prev(val) {
      if (val != 0) {
        this.comp[val] = false;
        this.comp[val - 1] = true;
      }
    },
    next(val) {
      console.log(val, this.comp[val], val + 1, this.comp[val + 1]);
      console.log(val + "nexted");
      this.comp[val] = false;
      this.comp[val + 1] = true;
      console.log(val, this.comp[val], val + 1, this.comp[val + 1]);
    },
    setTime() {
      ++this.totalSeconds;
      this.secondsLabel.innerHTML = this.pad(this.totalSeconds % 60);
      this.minutesLabel.innerHTML = this.pad(parseInt(this.totalSeconds / 60));
    },

    pad(val) {
      var valString = val + "";
      if (valString.length < 2) {
        return "0" + valString;
      } else {
        return valString;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
