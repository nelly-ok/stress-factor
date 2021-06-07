<template>
  <div class="home">
    <h1>Citations</h1>
    <p>
      Drug incarceration
    </p>
    <a href="https://www.americanprogress.org/issues/criminal-justice/reports/2018/06/27/452819/ending-war-drugs-numbers/
">https://www.americanprogress.org/issues/criminal-justice/reports/2018/06/27/452819/ending-war-drugs-numbers/
    </a>


    <p>
      Hate Crime stats
    </p>
    <a href="https://ucr.fbi.gov/hate-crime/2019/topic-pages/victims
">https://ucr.fbi.gov/hate-crime/2019/topic-pages/victims
    </a>



    <p>
      Trans violence
    </p>
    <a href="https://www.hrc.org/resources/violence-against-the-trans-and-gender-non-conforming-community-in-2020
">https://www.hrc.org/resources/violence-against-the-trans-and-gender-non-conforming-community-in-2020
    </a>



    <p>
      Fatal police shooting
    </p>
    <a href="https://www.bmj.com/company/newsroom/fatal-police-shootings-of-unarmed-black-people-in-us-more-than-3-times-as-high-as-in-whites/
">https://www.bmj.com/company/newsroom/fatal-police-shootings-of-unarmed-black-people-in-us-more-than-3-times-as-high-as-in-whites/
    </a>



    <p>
      Single parent
    </p>
    <a href="https://datacenter.kidscount.org/data/tables/107-children-in-single-parent-families-by-race#detailed/1/any/false/1729,37,871,870,573,869,36,868,867,133/10,11,9,12,1,185,13/432,431

">https://datacenter.kidscount.org/data/tables/107-children-in-single-parent-families-by-race#detailed/1/any/false/1729,37,871,870,573,869,36,868,867,133/10,11,9,12,1,185,13/432,431

    </a>





    <p>
      Education statistics
    </p>
    <a href="https://nces.ed.gov/programs/digest/d20/tables/dt20_104.20.asp
">https://nces.ed.gov/programs/digest/d20/tables/dt20_104.20.asp
    </a>





    <p>
      Education pays
    </p>
    <a href="https://www.bls.gov/emp/chart-unemployment-earnings-education.htm
">https://www.bls.gov/emp/chart-unemployment-earnings-education.htm
    </a>





    <p>
      Household Income
    </p>
    <a href="https://www.statista.com/statistics/203207/percentage-distribution-of-household-income-in-the-us-by-ethnic-group/
">https://www.statista.com/statistics/203207/percentage-distribution-of-household-income-in-the-us-by-ethnic-group/
    </a>





    <p>
      Statistics in Blue
    </p>
    <a href="https://www.youtube.com/watch?v=eCeAzhKobk8&t=332s
">https://www.youtube.com/watch?v=eCeAzhKobk8&t=332s
    </a>



    <NextButton :hideRight="true" @prev="prev" @next="next" />
  </div>
</template>

<script>

import NextButton from './NextButton'

export default {
  
  name: "Video1",
  components: {
    NextButton
  },
  props: {
    source: String,
    header: String,
    Right: Boolean
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

p {
  margin-top: 2em;
}

</style>
