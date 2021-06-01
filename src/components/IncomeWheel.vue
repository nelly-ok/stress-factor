<template>
  <div class="home">
    <h1>Spin the income wheel</h1>
    <img class="wheel bg" src="../assets/img/wheel-bg.png" alt="" srcset="" />
    <img
      class="wheel fg"
      id="FG"
      src="../assets/img/wheel-fg.png"
      alt=""
      srcset=""
    />
    <NextButton @prev="prev" @next="next" />
    <div class="results">
      <button type="button" class="btn btn-success" @click="spin">Spin</button>
      <p>Result: {{result}}</p>
      <p v-if="result">The median household income for Black Americans is $41,000</p>
      <p>{{incomeComparison}}</p>
    </div>
  </div>
</template>

<script>
import NextButton from "./NextButton.vue";

export default {
  name: "IncomeWheel",
  components: {
    NextButton,
  },
  props: {
    msg: String,
  },
  data() {
    return {
      result: "",
      incomeComparison: "",
      interval: false
    }
  },
  methods: {
    spin() {
      var deg = 0;
      this.interval = setInterval(function () {
        deg +=20;
        var wheel = document.getElementById("FG");
        wheel.style.webkitTransform = "rotate(" + deg + "deg)";
        wheel.style.mozTransform = "rotate(" + deg + "deg)";
        wheel.style.msTransform = "rotate(" + deg + "deg)";
        wheel.style.oTransform = "rotate(" + deg + "deg)";
        wheel.style.transform = "rotate(" + deg + "deg)";
      }, 100);

      

      //Stop the functions after 1 minute.
      setTimeout(this.incomeRandom, 3000);
    },
    prev() {
      this.$emit("prev");
    },
    next() {
      this.$emit("next");
    },
    incomeRandom(){
      clearInterval(this.interval);

      //https://www.statista.com/statistics/203207/percentage-distribution-of-household-income-in-the-us-by-ethnic-group/
      let rand = Math.floor(Math.random() * 101)+1; //pick a random number between 1 and 100
      if (rand <= 17) {
        this.result = "Under 15,000";
        this.incomeComparison = "You are below the median";
        console.log("stressing");
        this.$emit("stress", 5);
      } 
      else if (rand > 17 && rand <= 29) {
        this.result = "15,000 to 24,999";
        this.incomeComparison = "You are below the median";
        console.log("stressing");
        this.$emit("stress", 5);
      } 
      else if (rand > 29 && rand <= 40) {
        this.result = "25,000 to 34,999";
        this.incomeComparison = "You are below the median";
        console.log("stressing");
        this.$emit("stress", 5);
      } 
      else if (rand > 40 && rand <= 54) {
        this.result = "35,000 to 49,999";
        this.incomeComparison = "You are about median";
      } 
      else if (rand > 54 && rand <= 71) {
        this.result = "50,000 to 74,999";
        this.incomeComparison = "You are above the median";
      } 
      else if (rand > 71 && rand <= 81) {
        this.result = "75,000 to 99,999";
        this.incomeComparison = "You are above the median";
      } 
      else if (rand > 81 && rand <= 92) {
        this.result = "100,000 to 149,999";
        this.incomeComparison = "You are above the median";
      } 
      else if (rand > 92 && rand <= 96) {
        this.result = "150,000 to 199,999";
        this.incomeComparison = "You are above the median";
      } 
      else if (rand > 96 && rand <= 101) {
        this.result = "200,000 and over";
        this.incomeComparison = "You are above the median";
      }
    }
  },
};
</script>
ß
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wheel {
  width: 300px;
  position: absolute;
  
}
.results {
  position: relative;
    bottom: -5em;
}

.bg {
  z-index: 3;
}

.home h1 {
  position: relative;
  top: -3em;
}
</style>
