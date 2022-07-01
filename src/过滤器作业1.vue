<template>
  <div>
    <div>国内网站：粉丝数量{{ count | rounding("千") }}</div>
    <div>国外网站：粉丝数量{{ count | rounding("万") }}</div>
  </div>
</template>

<script>
export default {
  name: "Demo04App",
  // 定义一个局部过滤器
  filters: {
    rounding(val, unit) {
      if (unit === "千") {
        return val / 1000 + unit;
      } else {
        return val / 10000 + unit;
      }
    },
  },

  data() {
    return {
      count: 1876986,
    };
  },

  mounted() {},

  methods: {},
};
</script>

<style lang="scss" scoped>
</style>