<template>
  <section>
    <div class="header" v-if="startedFlag">
      <div class="time" @click="openTimerNotif">
        <label id="minutes">00</label>:<label id="seconds">00</label> 
      </div>
      <div class="timer-popup" id="TimerPopup">
        <p>Each minute represents a day. This corresponds to certain events that will be triggered</p>
        <button type="button" class="btn btn-primary" style="margin-left: 1em;" @click="closeTimerNotif">
          X
        </button>
      </div>
      <div class="gauge">
        <h6>Stress Level</h6>
        <img src="../src/assets/img/gauge.png" alt="" srcset="">
        <h6>{{this.stressLevel}}</h6>
      </div>
    </div>
    <div class="fatal-shootings" id="FatalShootings">
      <p>Every 1 day and 9 and a half hours, a Black person is fatally shot by a police officer</p>
      <p>Of the 5300+ fatal police shooting reported by the Washington Post from 2015 to May 2020, 51% were white, 27% were Black, and 19% were hispanic. Despite Black people making up 13% of the U.S population. Fatal shootings of unarmed black people are 3 times as high as whites.</p>
      <button type="button" class="btn btn-primary" style="margin-left: 1em;" @click="closeFatal">
          X
        </button>
        <button type="button" class="btn btn-primary" style="margin-left: 1em;" @click="stopFatal">
          Stop fatal shooting notifications
        </button>
    </div>
    <Home v-if="home" @started="started" @start="start" msg="Welcome to Your Vue.js App" />
    <Stress v-if="comp[0]" @prev="prev(0)" @next="next(0)" />
    <Stat1 v-if="comp[1]" @prev="prev(1)" @next="next(1)" />
    <Stat2 v-if="comp[2]" @prev="prev(2)" @next="next(2)" />
    <Stat3 v-if="comp[3]" @prev="prev(3)" @next="next(3)" />
    <Stat4 v-if="comp[4]" @prev="prev(4)" @next="next(4)" />
    <Stat5 v-if="comp[5]" @prev="prev(5)" @next="next(5)" />
    <IncomeWheel v-if="comp[6]" @prev="prev(6)" @next="next(6)" @stress="stress"/>
    <Video v-if="comp[7]" @prev="prev(7)" @next="next(7)" header="Depression, Anxiety and Money Problems" source="https://www.youtube.com/embed/hmAjftS73QA"/>
    <EducationWheel v-if="comp[8]" @prev="prev(8)" @next="next(8)" />
    <Video v-if="comp[9]" @prev="prev(9)" @next="next(9)" header="Coping with Stress" source="https://www.youtube.com/embed/rWzDq2318g8"/>
    <LifeWheel v-if="comp[10]" @prev="prev(10)" @next="next(10)" />
  </section>
</template>

<script>
import Home from "./components/Home/Home.vue";
import Stress from "./components/Stress.vue";
import Stat1 from "./components/Stat1.vue";
import Stat2 from "./components/Stat2.vue";
import Stat3 from "./components/Stat3.vue";
import Stat4 from "./components/Stat4.vue";
import Stat5 from "./components/Stat5.vue";
import IncomeWheel from "./components/IncomeWheel.vue";
import LifeWheel from "./components/LifeWheel.vue";
import EducationWheel from "./components/EducationWheel.vue";
import Video from "./components/Video"

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
    IncomeWheel,
    EducationWheel,
    Video,
    LifeWheel,
  },
  data() {
    return {
      home: true,
      comp0: false,
      comp1: false,
      comp: { 0: false, 1: false, 2: false, 3: false, 4: false, 5: false, 6: false, 7: false, 8: false, 9: false, 10: false },
      minutesLabel: false,
      secondsLabel: false,
      totalSeconds: 0,
      timerPopup: false,
      fatal: true,
      fatalDiv: false,
      startedFlag: false,
      stressLevel: 0
    };
  },
  mounted() {
    //https://stackoverflow.com/questions/5517597/plain-count-up-timer-in-javascript
    

  },
  methods: {
    start() {
      console.log("start");
      this.home = false;
      this.comp[0] = true;
    },
    started() {
      this.startedFlag = true;
      setTimeout(this.startTime, 1000);
    },
    prev(val) {
      if (val != 0) {
        this.comp[val] = false;
        this.comp[val - 1] = true;
      }
      else {
        this.comp[val] = false
        this.home = true
      }
    },
    next(val) {
      if (val < 10){
        this.comp[val] = false;
        this.comp[val + 1] = true;
      }
    },
    setTime() {
      ++this.totalSeconds;
      this.secondsLabel.innerHTML = this.pad(this.totalSeconds % 60);
      this.minutesLabel.innerHTML = this.pad(parseInt(this.totalSeconds / 60));
    },
    startTime(){
      //https://stackoverflow.com/questions/5517597/plain-count-up-timer-in-javascript
      this.minutesLabel = document.getElementById("minutes");
      this.secondsLabel = document.getElementById("seconds");
      setInterval(this.setTime, 1000);
      setInterval(this.fatalShooting, 83220);
      this.timerPopup = document.getElementById("TimerPopup");
      this.fatalDiv = document.getElementById("FatalShootings")
    },
    pad(val) {
      var valString = val + "";
      if (valString.length < 2) {
        return "0" + valString;
      } else {
        return valString;
      }
    },
    openTimerNotif() {
      this.timerPopup.style.display = "flex";
    },
    closeTimerNotif() {
      this.timerPopup.style.display = "none";
    },
    closeFatal(){
      this.fatalDiv.style.display = "none";
    },
    stopFatal(){
      this.fatal = false
      this.closeFatal();
    },
    fatalShooting(){
      if (this.fatal) {
        this.fatalDiv.style.display = "block";
        setTimeout(() => {
          this.closeFatal();
        }, 15000)
      }
    },
    stress(value){
      this.stressLevel += value;
      console.log(this.stressLevel, value)
    }
  },
};
</script>

<style>
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif; */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-family: 'Odibee Sans', cursive;
}

body {
  font-family: 'Odibee Sans', cursive !important;
}

.gauge {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.gauge img {
  width: 75px
}
.header {
  display: flex;
  width: 100%;
  justify-content: space-between;
  padding: 1em;
  height: 20vh;
}

.timer-popup{
  position: absolute;
  display: none;
  left: 5em;
  background-color: yellow;
  padding: 1em;
}

.home {
  display: flex;
  padding: 4em;
  flex-direction: column;
  align-items: center;
  height: 80vh;
  justify-content: space-around;
}


.fatal-shootings {
  width: 700px;
  margin-left: 2em;
  position: absolute;
  display: none;
  top: 6em;
  padding: 1em;
  background-color: grey;
}

.stat-img {
  width: 55%;
}
</style>
