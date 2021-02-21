<template>
    <fieldset class="ticker" :class="'cur-' + currency" :title="name">
      <legend>{{ secid }}</legend>
      <span>{{ value }}</span>
    </fieldset>
</template>

<script>
import axios from "axios";
export default {
  name: "TheTicker",
  props: ["secid", "board"],
  data() {
    return { moex: [] };
  },
  computed: {
    name() {
      return this.moex[0];
    },
    value() {
      return this.moex[1];
    },
    currency() {
      return this.moex[2];
    },
  },
  mounted() {
    let url =
      "https://iss.moex.com/iss" +
      "/engines/stock" +
      "/markets/shares" +
      "/boards/" +
      this.board +
      "/securities/" +
      this.secid +
      ".json?iss.meta=off&iss.only=securities&securities.columns=SECNAME,PREVADMITTEDQUOTE,CURRENCYID";
    axios
      .get(url)
      .then((response) => (this.moex = response.data.securities?.data[0]))
      .catch((e) => {
        this.errors.push(e);
      });
  },
};
</script>

<style lang="sass" scoped>
@import '../mq'

.cur-USD
  border: 1px solid darkgreen
  & span::before
    color: darkgreen
    content: '$'

.cur-SUR
  border: 1px solid darkred
  & span::after
    color: darkred
    content: '₽'

.ticker
  display: inline-block
  padding: 10px
  margin: 10px
  & legend
   font-weight: bolder
</style>