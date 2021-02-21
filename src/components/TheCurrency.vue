<template>
  <fieldset class="currency" :class="'cur-' + secid" :title="moex">
    <legend>{{ secid }}</legend>
    <span>{{ value }}</span>
  </fieldset>
</template>

<script>
import axios from "axios";
export default {
  name: "TheCurrency",
  props: ["secid", "to"],
  data() {
    return { moex: [] };
  },
  computed: {
    date() {
      let d = new Date();
      d.setDate(d.getDate() - 10);
      const ye = new Intl.DateTimeFormat("en", { year: "numeric" }).format(d);
      const mo = new Intl.DateTimeFormat("en", { month: "2-digit" }).format(d);
      const da = new Intl.DateTimeFormat("en", { day: "2-digit" }).format(d);

      return `${ye}-${mo}-${da}`;
    },
    value() {
      return this.moex ? this.moex[0] : "";
    },
  },
  mounted() {
    let url =
      "https://iss.moex.com/iss/statistics" +
      "/engines/futures" +
      "/markets/indicativerates" +
      "/securities/" +
      this.secid +
      "/" +
      this.to +
      ".json?iss.meta=off&iss.only=securities&securities.columns=rate,tradedate,tradetime&from=" +
      this.date;
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

.currency
  display: inline-block
  padding: 10px
  margin: 10px
  & legend
    font-weight: bolder
</style>