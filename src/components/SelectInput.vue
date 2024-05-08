<script>
export default {
  name: "SelectInput",
  props: ["Valute"],
  data() {
    return {};
  },
};
</script>

<template>
  <div class="row justify-content-center ">
    <div class="col-4">
      <select name="Val1" id="Val1" class="w-100">
        <option
          v-for="singleValuta in Valute"
          :value="singleValuta"
          :selected="singleValuta == 'EUR'"
        >
          {{ singleValuta }}
        </option>
      </select>
    </div>
    <div class="col-4 ps-0 ">
      <select name="Val2" id="Val2" class="w-100">
        <option
          v-for="singleValuta in Valute"
          :value="singleValuta"
          :selected="singleValuta == 'USD'"
        >
          {{ singleValuta }}
        </option>
      </select>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
