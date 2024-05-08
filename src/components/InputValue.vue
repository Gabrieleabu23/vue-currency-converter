<script>
export default {
  name: "InputValue",
  props: ["amount"],
  data() {
    return {};
  },
  methods: {
    debounce(Cifra) {
      clearTimeout(this.timer);
      this.timer = setTimeout(() => {
        this.elapsedTime = 0;
        this.$emit('input', Cifra);
      }, 700);
      this.elapsedTime++;
    },
  },
};
</script>

<template>
  <div class="col-3">
    <input
      type="number"
      name="amount"
      id="amount"
      :placeholder="amount"
      @input="debounce($event.target.value)"
    />
    <!-- &#8364 hex code euro -->
  </div>
</template>

<style lang="scss" scoped></style>
