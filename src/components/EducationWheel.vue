<template>
  <div class="home">
    <h1>Spin the education wheel</h1>
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
      <p>{{educationComparison}}</p>
      <a href="hhttps://nces.ed.gov/programs/digest/d20/tables/dt20_104.20.asp">
      <button type="button" id="Right" class="btn btn-success" >
        Click to see education by race and gender chart
      </button></a>
    </div>
  </div>
</template>

<script>
import NextButton from "./NextButton.vue";

export default {
  name: "EducationWheel",
  components: {
    NextButton,
  },
  props: {
    msg: String,
    gender: String
  },
  data() {
    return {
      result: "",
      educationComparison: "",
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
      setTimeout(this.educationRandom, 3000);
    },
    prev() {
      this.$emit("prev");
    },
    next() {
      this.$emit("next");
    },
    educationRandom(){
      clearInterval(this.interval);

      //https://nces.ed.gov/programs/digest/d20/tables/dt20_104.20.asp
      let education = {
        woman: {
          high: 96,
          associates: 43,
          bachelors: 33,
          masters: 7, 
          highComp: "About 96% of Black women have a High School Diploma or higher",
          assocComp: "About 43.2% of Black women have an Associates degree or higher compared with White women at 62.4% and 50% of all races and gender",
          bachComp: "About 32.6% of Black women have an Bachelors degree or higher compared with White women at 50.1% and 39.2% of all races and gender",
          masComp: "About 7.3% of Black women have an Masters degree or higher compared with White women at 13.3% and 9.4% of all races gender",
        },
        man: {
          high: 94,
          associates: 30,
          bachelors: 23,
          masters: 3, 
          highComp: "About 93.7% of Black men have a High School Diploma or higher",
          assocComp: "About 29.5% of Black men have an Associates degree or higher compared with Black women at 43.2% and White men at 50.5%",
          bachComp: "About 22.6% of Black men have an Bachelor degree or higher compared with Black women at 32.6.2% and White men at 39.2%",
          masComp: "About 3.3% of Black men have an Masters degree or higher compared with Black women at 7.3.2% and White men at 6.6%"},
        both: {
          high: 95,
          associates: 37,
          bachelors: 28,
          masters: 5, 
          highComp: "About 95% of Black people have a High School Diploma or higher",
          assocComp: "About 36.5% of Black people have an Associates degree or higher compared with 56.3% of Whites and 50% of all races",
          bachComp: "About 27.7% of Black people have an Bachelors degree or higher compared with 44.66% of Whites and 39.2% of all races",
          masComp: "About 5.3% of Black people have an Associates degree or higher compared with 9.9% of Whites and 9.4% of all races",
        }
      };

      
      let edu = null;
      console.log()
      if (this.gender == "man" || this.gender == "woman"){
        edu = education[this.gender];
      }
      else {
        edu = education.both
      }

      let rand = Math.floor(Math.random() * 101)+1; //pick a random number between 1 and 100
      if (rand <= edu.masters) {
        this.result = "Masters degree or higher";
        this.educationComparison = edu.masComp;
      } 
      else if (rand > edu.masters && rand <= edu.bachelors) {
        this.result = "Bachelors degree";
        this.educationComparison = edu.bachComp;
      } 
      else if (rand > edu.bachelors && rand <= edu.associates) {
        this.result = "Associates degree";
        this.educationComparison = edu.assocComp;
      } 
      else if (rand > edu.associates && rand <= edu.high) {
        this.result = "High School";
        this.educationComparison = edu.highComp;
        console.log("stressing");
        this.$emit("stress", 5);
      } 
      else if (rand > edu.high && rand <= 101) {
        this.result = "Less than High School";
        this.educationComparison = edu.highComp;
        console.log("stressing");
        this.$emit("stress", 5);
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
