<template>
  <div>
    <TheTicker v-for="ticker in tickers" :key="ticker.secid" v-bind="ticker" />
    <!--
    <hr />
    SUR: <input v-model="up.sur" /> USD: <input v-model="up.usd" />
    <hr />
    -->
    <TheCurrency
      v-for="currency in currencies"
      :key="currency.secid"
      v-bind="currency"
    />
  </div>
</template>

<script>
import TheTicker from "./TheTicker.vue";
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
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
