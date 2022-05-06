<template>
  <div>子组件说:{{ props.title }}</div>
  <button @click="toEmits">自定义事件暴露数据</button>
</template>

<script setup>
// 组件通信:在<script setup>中必须使用 defineProps 和 defineEmits API 来替代 props 和 emits
// 自定义事件使用 defineEmits    属性值传递使用 defineProps
import { ref } from "vue";
console.log('子组件setup')
const props = defineProps({
  title: {
    type: String,
  },
});
const name = ref("我是子组件");
const emits = defineEmits(["childFn"]);
const toEmits = () => {
  //2、触发父组件中暴露的childFn方法并携带数据
  emits("childFn", name.value);
};
console.log(props.title);
// 使用 <script setup> 的组件，父组件是无法通过ref 或者 $parent 获取到子组件的ref等响应数据，需要通过defineExpose 主动暴露
defineExpose({
  name,
//   toEmits,
});
</script>

<style></style>
