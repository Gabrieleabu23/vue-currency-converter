<script>
export default {
  name: "SelectInput",
  props: ["Valute", "val1", "val2"],
  data() {
    return {};
  },
  methods: {
    debounce(SelectedValuta, val) {
      clearTimeout(this.timer);
      this.timer = setTimeout(() => {
        this.elapsedTime = 0;
        this.$emit("input", {
          prop1: SelectedValuta,
          prop2: val
        });
      }, 700);
      this.elapsedTime++;
    },
  },
};
</script>

<template>
  <div class="row justify-content-center">
    <div class="col-4">
      <select
        name="Val1"
        id="Val1"
        class="w-100"
        @change="debounce($event.target.value, 'FROM')"
      >
        <option
          v-for="singleValuta in Valute"
          :value="singleValuta"
          :selected="singleValuta == val1"
          :disabled="singleValuta == val2"
        >
          {{ singleValuta }}
        </option>
      </select>
    </div>
    <div class="col-4 ps-0">
      <select
        name="Val2"
        id="Val2"
        class="w-100"
        @change="debounce($event.target.value, 'TO')"
      >
        <option
          v-for="singleValuta in Valute"
          :value="singleValuta"
          :selected="singleValuta == val2"
          :disabled="singleValuta == val1"
        >
          {{ singleValuta }}
        </option>
      </select>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
