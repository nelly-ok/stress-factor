<template>
    <div class="navigate">
      <button type="button" class="btn btn-success" @click="prev()">
        &lt; &lt;
      </button>
      <button type="button" class="btn btn-success" @click="next()">
        &gt; &gt;
      </button>
    </div>
</template>

<script>
export default {
  name: "Stat1",
  props: {
    msg: String,
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


</style>
