<template>
  <div>
    <h1>CGPA Calculator</h1>

    <div>
      <form validate @submit.prevent="submitit">
        <inputs v-for="(index, n) in n" :key="n" :n="index" />
        <button>submit</button>
      </form>
      {{ submit }}
      <div>
        <button @click="clear">clear</button> <br />
        <button class="add" @click="adds">+</button>
      </div>
    </div>
  </div>
</template>

<script>
import inputs from "./input";
export default {
  data() {
    return {
      hello: "hi",
      n: 1,
      result: "",
      value: "",
      unit: "",
      submit: ""
    };
  },
  components: {
    inputs
  },
  methods: {
    adds() {
      this.n += 1;
    },
    submitit(e) {
      const sumValues = obj =>
        Object.values(obj).reduce((a, b) => parseInt(a) + parseInt(b));
      const total = sumValues(this.total);
      const unit = sumValues(this.totalunit);
      this.submit = total / unit;
    },
    clear() {
      this.n = 0;
      // this.n = 1
      this.$store.commit("clear");
      this.submit = null;
    }
  },
  computed: {
    total() {
      return this.$store.state.values;
      //  this.unit = this.$store.state.unit
    },
    totalunit() {
      return this.$store.state.unit;
    }
  }
};
</script>

<style>
.add {
  width: 50px;
  height: 50px;
  border-radius: 100%;
  font-size: 25px;
  text-align: center;
  outline: none;
  color: white;
  background: skyblue;
}

/*button{
//   height: 35px;
//   border-radius:12px;
//   width:150px;
// }*/
</style>
