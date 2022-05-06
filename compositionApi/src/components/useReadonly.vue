// readonly 的使用
<template>
  <p>readonly</p>
  {{ money }}
  <div>{{car.branch}} -- {{car.price}}</div>
  <button @click="money++">++</button>
  <button @click="car.price--">--</button>
</template>

<script>
import { readonly, ref } from "vue";
export default {
  setup() {
    const money = ref(100);
    // readonly的实现: 实际就是Proxy的封装, 当set时, 不修改数据, 同时提示console.warn
    const car = readonly({
      branch:'宝马',
      price:1000000
    })
    console.log('readonly car: ', car)
    return {
      // money 只读,不可修改
      money: readonly(money),
      car
    }
  },
};
</script>

<style></style>
