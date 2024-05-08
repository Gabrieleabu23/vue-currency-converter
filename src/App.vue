<script>
import axios from "axios";
import SelectInput from "./components/SelectInput.vue";
export default {
  components: {
    SelectInput
  },
  data() {
    return {
      valute: [],
    };
  },
  methods: {
    callApiValute() {
      let x = this;
      axios
        .get("https://api.frankfurter.app/latest")
        .then(function (response) {
          // debug
          console.log(response.data);
          x.valute.push(response.data.base);
          for (const element in response.data.rates) {
            x.valute.push(element);
          }
          // debug
          // console.log(x.valute);
        })
        .catch(function (error) {
          console.log(error);
        });
    },
  },
  mounted() {
    this.callApiValute();
  },
};
</script>

<template>
<SelectInput :Valute="this.valute"/>
</template>

<style lang="scss"></style>
