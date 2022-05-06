<template>
  <div>reactive222222222</div>
  <div>{{ car.brand }} -- {{ car.color }}</div>
  <div>{{ brand }} -- {{color }}</div>
</template>

<script>
import { reactive, toRefs } from "vue";
export default {
  setup() {
    const car = reactive({
      brand: "奔驰",
      color: "blue",
    });
    setTimeout(() => {
      car.brand = "宝马";
    }, 2000);
    // 将响应式对象state转化成普通对象,同时将对象的每一个属性转成ref,生成新的响应式数据
    console.log(111,{...car});
    console.log(111,toRefs(car));
    return {
        // 直接使用扩展运算符会导致state中本来是简单类型的money丢失响应式,此时要使用到 toRefs
        ...car,
      car,
    };
  },
};
</script>

<style></style>
