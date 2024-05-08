<script>
export default {
  name: "Result",
  props: ["conversionAmount",'currency'],
  data() {
    return {};
  },
  methods: {
    currency() {
      const currencyFormatter = new Intl.NumberFormat("it-IT", {
        style: "currency",
        currency: this.currency // Codice della valuta da formattare
      });
      const formattedAmount = currencyFormatter.format(this.conversionAmount);
      return formattedAmount;
    },
  },
};
</script>

<template>
  <h4 v-if="conversionAmount != 0">
    Risultato:  {{ currency() }}
  </h4>
  <h6 v-else>Caricamento....</h6>
</template>

<style lang="scss" scoped></style>
