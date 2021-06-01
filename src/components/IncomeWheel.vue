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
      result: ""
    }
  },
  methods: {
    spin() {
      var deg = 0;
      const interval = setInterval(function () {
        deg +=20;
        var wheel = document.getElementById("FG");
        wheel.style.webkitTransform = "rotate(" + deg + "deg)";
        wheel.style.mozTransform = "rotate(" + deg + "deg)";
        wheel.style.msTransform = "rotate(" + deg + "deg)";
        wheel.style.oTransform = "rotate(" + deg + "deg)";
        wheel.style.transform = "rotate(" + deg + "deg)";
      }, 100);



      //Stop the functions after 1 minute.
      setTimeout(function () {
        clearInterval(interval);
      }, 3000);
    },
    prev() {
      this.$emit("prev");
    },
    next() {
      this.$emit("next");
    },
    incomeRandom(){
      let rand = Math.floor(Math.random() * 101)+1; //pick a random number between 1 and 100
      if (rand <= 17) {
        console.log("Under 15,000")
      } 
      else if (rand > 17 && rand <= 29) {
        console.log("15,000 to 24,999")
      } 
      else if (rand > 29 && rand <= 40) {
        console.log("25,000 to 34,999")
      } 
      else if (rand > 40 && rand <= 54) {
        console.log("35,000 to 49,999")
      } 
      else if (rand > 54 && rand <= 71) {
        console.log("50,000 to 74,999")
      } 
      else if (rand > 71 && rand <= 81) {
        console.log("75,000 to 99,999")
      } 
      else if (rand > 81 && rand <= 92) {
        console.log("100,000 to 149,999")
      } 
      else if (rand > 92 && rand <= 96) {
        console.log("150,000 to 199,999")
      } 
      else if (rand > 96 && rand <= 101) {
        console.log("200,000 and over")
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
