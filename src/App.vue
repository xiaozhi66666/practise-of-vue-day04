<template>
  <div id="app">
    <table class="tb">
      <tr>
        <th><input type="checkbox" v-model="isAll" />全选</th>
        <th>商品</th>
        <th>单价</th>
        <th>数量</th>
        <th>小记</th>
        <th>操作</th>
      </tr>
      <!-- 循环渲染的元素tr -->
      <tr v-for="item in list" :key="item.id">
        <td><input type="checkbox" v-model="item.c" /></td>
        <td>{{ item.name }}</td>
        <td>{{ item.price }}</td>
        <td>
          <button @click="item.count--">-</button
          ><input type="text" v-model="item.count" /><button
            @click="item.count++"
          >
            +
          </button>
        </td>
        <td>{{ item.count * item.price }}</td>
        <td><button>删除</button></td>
      </tr>

      <tr v-if="list.length === 0">
        <td colspan="6">没有数据咯~</td>
      </tr>
    </table>
    <br />
    <button @click="del">删除选中商品</button>
    <button @click="clearFn">清理购物车</button>
    <br />
    <div style="margin-top: 20px">
      <h2>统计</h2>
      <p>已经选中商品件数{{ totalCount }}</p>
      <p>总价{{ totalPrice == 0 ? 0 : totalPrice | priceInit }}</p>
    </div>
  </div>
</template>

<script>
export default {
  // 定义一个过滤器过滤价格单位
  filters: {
    priceInit(val) {
      return val / 10000 + "万";
    },
  },
  data() {
    return {
      list: [
        {
          id: 1,
          name: "奔驰",
          price: 20000,
          time: "2020-08-01",
          count: 0,
          c: false,
        },
        {
          id: 2,
          name: "宝马",
          price: 30000,
          time: "2020-08-02",
          count: 0,
          c: false,
        },
        {
          id: 3,
          name: "奥迪",
          price: 120000,
          time: "2020-08-03",
          count: 0,
          c: false,
        },
      ],
    };
  },
  methods: {
    // 删除功能
    del() {
      // 删除按钮 - 得到索引, 删除数组里元素
      const arr = this.list.filter((item) => item.c === false);
      this.list = arr;
      if (this.list.length === 0) return (this.isAll = true);
    },
    // 清空购物车功能
    clearFn() {
      this.list = [];
      this.isAll = false;
    },
  },
  computed: {
    // 计算属性(全选框状态)
    isAll: {
      set(val) {
        this.list.forEach((item) => (item.c = val));
      },
      get() {
        return this.list.length == 0
          ? false
          : this.list.every((item) => item.c === true);
      },
    },
    // 获取总数量
    totalCount() {
      const arr = this.list.filter((item) => item.c === true);
      // console.log(arr);
      return arr.reduce((sum, item) => (sum += item.count), 0);

      // console.log(arr);
    },
    // 获取总价格
    totalPrice() {
      const arr = this.list.filter((item) => item.c === true);
      return arr.reduce((sum, item) => (sum += item.count * item.price), 0);
    },
  },
};
</script>

<style>
#app {
  width: 600px;
  margin: 10px auto;
}

.tb {
  border-collapse: collapse;
  width: 100%;
}

.tb th {
  background-color: #0094ff;
  color: white;
}

.tb td,
.tb th {
  padding: 5px;
  border: 1px solid black;
  text-align: center;
}

.add {
  padding: 5px;
  border: 1px solid black;
  margin-bottom: 10px;
}
</style>
