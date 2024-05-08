<script>
import axios from "axios";
import SelectInput from "./components/SelectInput.vue";
import InputValue from "./components/InputValue.vue";
import Result from "./components/Result.vue";
import { watch } from "vue";
export default {
  components: {
    SelectInput,
    InputValue,
    Result,
  },
  data() {
    return {
      valute: [],
      val1: "EUR",
      val2: "USD",
      amount: 1,
      link: "",
      flag: 0,
      conversionAmount: 0,
      isLoading: false,
    };
  },
  methods: {
    async callApiValute() {
            if (this.flag == 1) {
        this.link = `https://api.frankfurter.app/latest?amount=${this.amount}&from=${this.val1}&to=${this.val2}`;
      } else {
        this.link = `https://api.frankfurter.app/latest?amount=${this.amount}`;
      }
      
      try {
        const response = await axios.get(this.link);
        // debug
        // console.log(response.data);
        if (this.flag == 0) {
          this.valute.push(response.data.base);
          for (let element in response.data.rates) {
            this.valute.push(element);
          }
        }
        this.conversionAmount = response.data.rates[this.val2];
        this.conversionAmount = parseFloat(this.conversionAmount.toFixed(2));
        console.log(this.conversionAmount);
        // debug
        // console.log(this.valute);
        
      } catch (error) {
        console.log(error);
      } finally {
      }
    },
    updateAmount(newAmount) {
      this.flag = 1;
      this.amount = newAmount;
      console.log("valore aggiornato" + newAmount);
      this.callApiValute();
    },

    updateSelect(SelectData) {
      this.flag = 1;
      console.log(SelectData);
      // PRENDO PROPS1 CHE È LA VALUTA DA SOSTITUIRE AL POSTO DI VAL ( CHE È PROPS2)
      if (SelectData.prop2 == 'TO') {
        console.log(SelectData.prop1);
        this.val2 = SelectData.prop1;
      } else if(SelectData.prop2 == 'FROM') {
        this.val1 = SelectData.prop1;
      }
        this.callApiValute();
    },
  },
  mounted() {
    this.flag = 0;
    this.callApiValute();
  },
};
</script>

<template>
  <div class="row justify-content-center" v-if="!this.isLoading">
    <InputValue :amount="this.amount" @input="updateAmount" />
    <SelectInput
      :Valute="this.valute"
      :val1="this.val1"
      :val2="this.val2"
      @input="updateSelect"
    />
    <Result :conversionAmount="this.conversionAmount" :currency="this.val2" />
  </div>
  <div v-else>Caricamento...</div>
</template>

<style lang="scss"></style>
