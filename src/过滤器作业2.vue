<template>
  <div>
    <div>时间：{{ time | timeInit("-") }}</div>
    <div>时间：{{ time | timeInit("/") }}</div>
  </div>
</template>

<script>
import moment from "moment";
export default {
  name: "Demo04App",

  data() {
    return {
      time: +new Date(),
    };
  },
  filters: {
    timeInit(val, s) {
      return moment(val).format("YYYY" + s + "MM" + s + "DD");
    },
  },

  mounted() {},

  methods: {},
};
</script>

<style lang="scss" scoped>
</style>