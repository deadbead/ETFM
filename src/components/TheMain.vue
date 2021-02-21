<template>
  <div>
    <TheTicker v-for="ticker in tickers" :key="ticker.secid" v-bind="ticker" />
    <!--
    <hr />
    SUR: <input v-model="up.sur" /> USD: <input v-model="up.usd" />
    <hr />
    -->
    <hr />
    <TheCurrency
      v-for="currency in currencies"
      :key="currency.secid"
      v-bind="currency"
      to="RUB"
    />
  </div>
</template>

<script>
import TheTicker from "./TheTicker.vue";
import TheCurrency from "./TheCurrency.vue";
export default {
  name: "Main view",
  data() {
    return {
      up: { usd: 0, sur: 0 },
      currencies: [{ secid: "USD" }, { secid: "SUR" }],
      tickers: [
        { secid: "TSPX", board: "TQTD" },
        { secid: "TMOS", board: "TQTF" },
        { secid: "TECH", board: "TQTD" },
        { secid: "TBIO", board: "TQTD" },
        { secid: "FXUS", board: "TQTF" },
        { secid: "FXIM", board: "TQTF" },
        { secid: "FXCN", board: "TQTF" },
        { secid: "FXWO", board: "TQTF" },
        { secid: "SBMX", board: "TQTF" },
        { secid: "DIVD", board: "TQTF" },
        { secid: "TIPO", board: "TQTD" },
        { secid: "FXGD", board: "TQTF" },
        { secid: "TGLD", board: "TQTD" },
      ],
    };
  },
  components: {
    TheTicker,
    TheCurrency,
  },
};
</script>

<style scoped>
</style>
