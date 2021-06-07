<template>
  <div class="home">
    <h1>{{header}}</h1>
    <div class="wheel-container">
      <img class="wheel bg" src="../assets/img/wheel-bg.png" alt="" srcset="" />
      <img
        class="wheel fg"
        id="FG"
        src="../assets/img/wheel-fg.png"
        alt=""
        srcset=""
      />
    </div>
    <NextButton @prev="prev" @next="next" />
    <div class="results">
      <button type="button" class="btn btn-success" @click="spin">Spin</button>
      <p>Result: {{result}}</p>
      <p v-if="result && !child">The median household income for Black Americans is $41,000</p>
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
    age: String
  },
  data() {
    return {
      result: "",
      incomeComparison: "",
      interval: false,
      header: "",
      child: false,
    }
  },
  mounted() {
    console.log(this.age)
    if (this.age == "5-10" || this.age == "10-18"){
      this.header = "Spin the single parent wheel"
      this.child = true
    }
    else {
      this.header = "Spin the income wheel"
    }
    console.log(this.child)
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
      if (this.child){
        console.log("child randomizer")
        setTimeout(this.singleRandom, 3000);
      }
      else {
        setTimeout(this.incomeRandom, 3000);
      }
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
    },
    singleRandom(){
      clearInterval(this.interval);

      //https://www.statista.com/statistics/203207/percentage-distribution-of-household-income-in-the-us-by-ethnic-group/
      let rand = Math.floor(Math.random() * 101)+1; //pick a random number between 1 and 100
      if (rand <= 64) {
        this.result = "single parent";
        this.incomeComparison = "64% of black children grow up in a single parent household";
        console.log("stressing");
        this.$emit("stress", 15);
      } 
      else {
        this.result = "both parents";
        this.incomeComparison = "64% of black children grow up in a single parent household. You were a bit lucky this time";
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

.wheel-container {
  position: relative;
    top: -150px;
    left: -150px;
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
