// 生命周期钩子函数
<template>
  <p>生命周期钩子函数</p>
  <p>{{money}}</p>
  <button @click="money++">money++</button>
</template>

<script>
import { ref,onBeforeMount, onMounted, onBeforeUpdate, onUpdated,onBeforeUnmount, onUnmounted} from 'vue';

export default {
  setup(){
    const money = ref(100)
    // 挂载前
    onBeforeMount(()=>console.log('onBeforeMount'))
    // 挂载后
    onMounted(()=>console.log('onMounted'))
    // 更新前
    onBeforeUpdate(()=>console.log('onBeforeUpdate'))
    // 更新后
    onUpdated(()=>console.log('onUpdated'))
    //  卸载前
    onBeforeUnmount(()=>console.log('onBeforeUnmount'))
    //  卸载后
    onUnmounted(()=>console.log('onUnmounted'))
    return {
      money
    }
  }

};
</script>

<style></style>
