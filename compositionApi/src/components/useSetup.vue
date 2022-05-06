// setup 的使用
<template>{{ car.brand }}:{{ car.color }}</template>

<script>
export default {
  setup() {
    // console.log("setup");
    // console.log(this);
    // 这个数据不是响应式的,要使用响应式的数据想要使用reactive
    const car = {
      brand: "奔驰",
      color: "blue",
    };
    setTimeout(() => {
      car.brand = "宝马";
      console.log(car.brand);
    }, 2000);
    // setup中返回数据暴露给组件使用
    return {
      car,
    };
  },
  beforeCreate() {
    console.log("beforeCreate");
    console.log(this.car);
  },
};
</script>

<style></style>
