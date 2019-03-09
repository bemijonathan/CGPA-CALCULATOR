<template>
  <div class="inputs">
    <div>
      <label for="course">Course</label><br />
      <input
        type="text"
        class="course-title"
        name="course"
        v-model="course"
        required
      />
    </div>

    <div>
      <label for="grades"> Grades </label><br />
      <select name="grades" required v-model="grade">
        <option value="5">A</option>
        <option value="4">B</option>
        <option value="3">C</option>
        <option value="2">D</option>
        <option value="1">E</option>
        <option value="0">F</option>
      </select>
    </div>

    <div>
      <label for="unit"> Credict Unit </label><br />
      <select name="unit" required v-model="unit">
        <option value="5">5</option>
        <option value="4">4</option>
        <option value="3">3</option>
        <option value="2">2</option>
        <option value="1">1</option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  props: ["n"],
  data() {
    return {
      unit: "",
      grade: "",
      course: "",
      total: "",
      key: ""
    };
  },
  created() {
    this.key = this.n;
    this.$watch(
      vm => [vm.unit, vm.grade],
      val => {
        this.total = parseInt(this.grade) * parseInt(this.unit).toString();
        var payload = {
          [this.n]: this.total
        };
        var unit = {
          [this.n]: this.unit
        };
        this.$store.commit("addTotal", payload);
        this.$store.commit("unit", unit);
      },
      { immediate: true }
    );
  }
};
</script>

<style>
.inputs {
  display: grid;
  grid-template-columns: auto auto auto;
  text-align: center;
}
</style>
