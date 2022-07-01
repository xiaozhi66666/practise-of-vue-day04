<!--局部过滤器-->
<template>
  <div>
    <p>原来的样子: {{ msg }}</p>
    <!-- 2. 过滤器使用
      语法: {{ 值 | 过滤器名字 }}
     -->
    <p>使用翻转过滤器: {{ msg | reverse }}</p>
    <p :title="msg | toUp">鼠标长停</p>
  </div>
</template>

<script>
export default {
  name: "Demo04App",

  data() {
    return {
      msg: "Hello, Vue",
    };
  },

  mounted() {},

  methods: {},
  filters: {
    toUp(val) {
      return val.toUpperCase();
    },
    reverse(val) {
      return val.split("").reverse().join("");
    },
  },
};
</script>

<style  scoped>
</style>