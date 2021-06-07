<template>
  <section>
    <div class="header" v-if="startedFlag">
      <div class="time" @click="openTimerNotif">
        <label id="minutes">00</label>:<label id="seconds">00</label> 
      </div>
      <div class="timer-popup" id="TimerPopup">
        <p>Each minute represents a day. This corresponds to certain events that will be triggered</p>
        <button type="button" class="btn btn-primary x-btn" style="margin-left: 1em;" @click="closeTimerNotif">
          X
        </button>
      </div>
      <div class="gauge">
        <h4>Stress Level</h4>
        <img src="../src/assets/img/gauge.png" alt="" srcset="">
        <h4>{{this.stressLevel}}</h4>
      </div>
    </div>

    <div v-if="notifCount.length" class="notif" id="Notifications">
      <div class="fatal-shootings notification" id="FatalShootings" v-if="fatalDiv">
        <p>Every 1 day and 9 and a half hours, a Black person is fatally shot by a police officer</p>
        <p>Of the 5300+ fatal police shooting reported by the Washington Post from 2015 to May 2020, 51% were white, 27% were Black, and 19% were hispanic. Despite Black people making up 13% of the U.S population. Fatal shootings of unarmed black people are 3 times as high as whites.</p>
          <div class="buttons">
            <button type="button" class="btn btn-primary x-btn" style="margin-left: 1em;" @click="closeFatal">
              X
            </button>
            <button type="button" class="btn btn-success" style="margin-left: 1em;" @click="stopFatal">
              Stop fatal shooting notifications
            </button>
          </div>
      </div>
      <div class="drugs notification" id="Drugs" v-if="drugsDiv">
        <p>About 17 Black people today have been arrested for drug possession. Every 83.33 seconds, a Black person is arrested for drug possesion. </p>
        <p>In America, every 25 seconds, someone is arrested for drug possession. Black people make up about 30 percent of all drug arrests, despite only being about 12.5 percent of substance users.</p>
          <div class="buttons">
            <button type="button" class="btn btn-primary x-btn" style="margin-left: 1em;" @click="closeDrugs">
              X
            </button>
            <button type="button" class="btn btn-success" style="margin-left: 1em;" @click="stopDrugs">
              Stop  drug arrest notifications
            </button>
          </div>
      </div>

      <div class="trans notification" id="Trans" v-if="transDiv">
        <p>About every 8 days and 7 hours, a transgender or gender non-conforming person is fatally shot or killed. </p>
        <p>2020 saw at least 44 transgender or gender non-conforming people fatally shot or violently killed. The majority these cases are Black and Latinx transgender women.</p>
          <div class="buttons">
            <button type="button" class="btn btn-primary x-btn" style="margin-left: 1em;" @click="closeTrans">
              X
            </button>
            <button type="button" class="btn btn-success" style="margin-left: 1em;" @click="stopTrans">
              Stop trans violence notifications
            </button>
          </div>
      </div>

      <div class="hate notification" id="Trans" v-if="hateDiv">
        <p>About every 3 hours and 40 minutes, a Black person is a victim of a race based hate crime.. </p>
        <p>Of the 4920 victims of race/ethnicity/ancestry motivated hate crimes, 48.5 were victims motivated by anti-Black of African American bias.</p>
          <div class="buttons">
            <button type="button" class="btn btn-primary x-btn" style="margin-left: 1em;" @click="closeHate">
              X
            </button>
            <button type="button" class="btn btn-success" style="margin-left: 1em;" @click="stopHate">
              Stop hate crime notifications
            </button>
          </div>
      </div>

    </div>
    <Home v-if="home" @started="started"  @unstarted="unstarted" @start="start" msg="Welcome to Your Vue.js App" />
    <Stress  v-if="comp[0]" @prev="prev(0)" @next="next(0)" />
    <Stat :header="stats[0].header" :img="getImg(stats[0].img)" v-if="comp[1]" @prev="prev(1)" @next="next(1)" />
    <Stat :header="stats[1].header" :img="getImg(stats[1].img)" v-if="comp[2]" @prev="prev(2)" @next="next(2)" />
    <Stat :header="stats[2].header" :img="getImg(stats[2].img)" v-if="comp[3]" @prev="prev(3)" @next="next(3)" />
    <Stat :header="stats[3].header" :img="getImg(stats[3].img)" v-if="comp[4]" @prev="prev(4)" @next="next(4)" />
    <Stat :header="stats[4].header" :img="getImg(stats[4].img)" v-if="comp[5]" @prev="prev(5)" @next="next(5)" />
    <IncomeWheel v-if="comp[6]" @prev="prev(6)" @next="next(6)" @stress="stress" :age="age"/>

    <div v-if="!child">
      <Video v-if="comp[7]" @prev="prev(7)" @next="next(7)" header="Depression, Anxiety and Money Problems" source="https://www.youtube.com/embed/hmAjftS73QA"/>
    </div>
    <div v-else>
      <Video v-if="comp[7]" @prev="prev(7)" @next="next(7)" header="7 Effects of Growing Up with a Single Parent" source="https://www.youtube.com/embed/bnPF2K1Dz7E"/>
    </div>

    <EducationWheel :gender="gender" v-if="comp[8]" @prev="prev(8)" @next="next(8)" @stress="stress"/>
    <EducationAnalysis :gender="gender" v-if="comp[9]" @prev="prev(9)" @next="next(9)" @stress="stress"/>

    <Video v-if="comp[10]" @prev="prev(10)" @next="next(10)" header="Images of Black people dying spur racial trauma" source="https://www.youtube.com/embed/WSi7Bp7LPsQ"/>
    <Video v-if="comp[11]" @prev="prev(11)" @next="next(11)" header="Experiencing Racial Trauma" source="https://www.youtube.com/embed/KsWacConZNw"/>

    
    <Video v-if="comp[12]" @prev="prev(12)" @next="next(12)" header="Coping with Stress" source="https://www.youtube.com/embed/rWzDq2318g8"/>
    <Video  v-if="comp[13]" @prev="prev(13)" @next="next(13)" header="How Toxic Stress Affects Us, and What We Can Do About It" source="https://www.youtube.com/embed/sutfPqtQFEc"/>
    <Video1  v-if="comp[14]" @prev="prev(14)" @next="next(14)" />


    <Breakdown v-if="breakdown" @destress="loadDestressor" />
    <Destressor v-if="destressor" @finishDestress="finishDestress" />
  </section>
</template>

<script>
import Home from "./components/Home/Home.vue";
import Stress from "./components/Stress.vue";
import Stat from "./components/Stat.vue";
import IncomeWheel from "./components/IncomeWheel.vue";
import EducationWheel from "./components/EducationWheel.vue";
import Video from "./components/Video"
import Video1 from "./components/Video1"

import EducationAnalysis from './components/EducationAnalysis'
import Breakdown from './components/Breakdown.vue'
import Destressor from './components/Destressor/Destressor.vue';

export default {
  name: "App",
  components: {
    Home,
    Stress,
    Stat,
    IncomeWheel,
    EducationWheel,
    Video,
    Video1,
    EducationAnalysis,
    Breakdown,
    Destressor
  },
  data() {
    return {
      gender: null,
      age: null,
      sex: null,
      child: false,
      home: true,
      comp0: false,
      comp1: false,
      comp: { 0: false, 1: false, 2: false, 3: false, 4: false, 5: false, 6: false, 7: false, 8: false, 9: false, 10: false, 11: false, 12: false, 13: false, 14: false},
      minutesLabel: false,
      secondsLabel: false,
      totalSeconds: 0,
      timerPopup: false,
      fatal: true,
      fatalDiv: false,
      drugs: true,
      drugsDiv: false,
      trans: true,
      transDiv: false,
      hate: true,
      hateDiv: false,
      startedFlag: false,
      stressLevel: 0,
      timeInt: false,
      fatInt: false,
      hateInt: false,
      transInt: false,
      drugsInt: false,
      breakdown: false,
      destressor: false,
      notifCount: ["dummy"],
      stats: [{
        header: "Next lets explore race. America (like most other countriess) has a race problem. Don’t believe? I’ll let the numbers do the talking.",
        img: "income"
      }, {
        header: "Now thats just income, money received on a regular basis. For wealth, the total value of assets, possesions, or money, the gap is even starker.",
        img: "Stat2" 
      }, {
        header: "",
        img: "Stat3"
      }, {
        header: "",
        img: "Stat4"
      }, {
        header: "",
        img: "Stat5"
      }, ]
      };
  },
  mounted() {
    //https://stackoverflow.com/questions/5517597/plain-count-up-timer-in-javascript
    this.notifCount.pop()

  },
  methods: {
    start(value) {
      console.log("start");
      this.home = false;
      this.comp[0] = true;
      this.gender = value.gender;
      this.age = value.age;
      this.sex = value.sex;
      if (this.age == "5-10" || this.age == "10-18"){
      this.child = true
    }
      console.log(value)
    },
    started() {
      this.startedFlag = true;
      setTimeout(this.startTime, 1000);
    },
    unstarted() {
      this.startedFlag = false;
      //https://stackoverflow.com/questions/8635502/how-do-i-clear-all-intervals
      clearInterval(this.fatInt);
      clearInterval(this.drugsInt);
      clearInterval(this.timeInt)
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
      if (val < 14){
        this.comp[val] = false;
        this.comp[val + 1] = true;
      }
    },
    getImg(name){
      var images = require.context('./assets/img/', false, /\.jpg$/)
      return images('./' + name + ".jpg")
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
      this.timeInt = setInterval(this.setTime, 1000);
      this.fatInt = setInterval(this.fatalShooting, 83220);
      this.drugsInt = setInterval(this.drugArrest, 60000);
      this.transInt = setInterval(this.transViolence, 82954);
      this.hateInt = setInterval(this.hateCrime, 15265);
      this.timerPopup = document.getElementById("TimerPopup");
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
      this.fatalDiv = false;
      for( var i = 0; i < this.notifCount.length; i++){ 
                                   
        if ( this.notifCount[i] == "fatal") { 
            this.notifCount.splice(i, 1); 
            i--; 
        }
    }
      console.log(this.notifCount)
    },
    stopFatal(){
      this.fatal = false
      this.closeFatal();
    },
    fatalShooting(){
      if (this.fatal) {
        if(!this.notifCount.includes("fatal")){
          this.notifCount.push("fatal")
        }
        this.fatalDiv = true;
        this.stress(10);
      }
    },
    closeDrugs(){
      this.drugsDiv = false;
      for( var i = 0; i < this.notifCount.length; i++){ 
                                   
        if ( this.notifCount[i] == "drugs") { 
            this.notifCount.splice(i, 1); 
            i--; 
        }
    }
      console.log(this.notifCount)
    },
    stopDrugs(){
      this.drugs = false
      this.closeDrugs();
    },
    drugArrest(){
      if (this.drugs) {
        if(!this.notifCount.includes("drugs")){
          this.notifCount.push("drugs")
        }
        this.drugsDiv = true;
        this.stress(10);
      }
    },
    closeTrans(){
      this.transDiv = false;
      for( var i = 0; i < this.notifCount.length; i++){ 
                                   
        if ( this.notifCount[i] == "trans") { 
            this.notifCount.splice(i, 1); 
            i--; 
        }
    }
      console.log(this.notifCount)
    },
    stopTrans(){
      this.trans = false
      this.closeTrans();
    },
    transViolence(){
      if (this.trans) {
        if(!this.notifCount.includes("trans")){
          this.notifCount.push("trans")
        }
        this.transDiv = true;
        this.stress(10);
      }
    },
    closeHate(){
      this.hateDiv = false;
      for( var i = 0; i < this.notifCount.length; i++){ 
                                   
        if ( this.notifCount[i] == "hate") { 
            this.notifCount.splice(i, 1); 
            i--; 
        }
    }
      console.log(this.notifCount)
    },
    stopHate(){
      this.hate = false
      this.closeHate();
    },
    hateCrime(){
      if (this.hate) {
        if(!this.notifCount.includes("hate")){
          this.notifCount.push("hate")
        }
        this.hateDiv = true;
        this.stress(10);
      }
    },
    stress(value){
      this.stressLevel += value;
      if (this.stressLevel >= 100){
        this.loadBreakdown();
      }
      console.log(this.stressLevel, value)
    },
    loadBreakdown() {
      this.breakdown = true
    },
    loadDestressor() {
      this.breakdown = false
      this.destressor = true
    },
    finishDestress(){
      this.destressor = false
      this.stressLevel = 0
    },
    arrayRemove(arr, value) { 
    
        return arr.filter(function(ele){ 
            return ele != value; 
        });
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
  transition: 0.3s;
}

html {
}

body {
  font-family: 'Odibee Sans', cursive !important;
  background-image: linear-gradient(to bottom,  #009cea, white);
  background-image: -webkit-linear-gradient(top,  #009cea, white);
  transition: 0.3s;
}

p {
  font-size: 1.25rem;
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
  left: 10em;
  background-color: #ffb64c;
  font-weight: 1.25rem;
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
  width: 45%;
  height: 45%;
  margin-left: 2em;
  display: block;
  top: 6em;
  padding: 1em;
  background-color: grey;
}

.notification {
  width: 45%;
  height: 45%;
  margin-left: 2em;
  display: block;
  top: 6em;
  padding: 1em;
  background-color: grey;
}

.notification .buttons {
  display: flex;
  justify-content: center;
  align-items: center;
}

.stat-img {
  width: 50%;
}

.btn-success{
  background-color: #00b379 !important;
  border-color: #00b379 !important;
}

.time {
  font-family: 'Orbitron', sans-serif;
  font-size: xx-large;
  transition: 0.3s;
}

.time:hover {
  font-size: xxx-large;
}

.form-select {
  font-size: 1.25rem !important;
}

.btn {
  font-size: 1.25rem !important;
}

.x-btn {
    width: 2rem !important;
    height: 2rem !important;
    display: flex !important;
    justify-content: center !important;
    align-items: center !important;
    border-radius: unset !important;
    background: red !important;
    border: red !important;
}
.notif {
  background: #333a;
  z-index: 4;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    display: flex;
    padding-top: 4em;
        flex-flow: row wrap;
}
</style>
