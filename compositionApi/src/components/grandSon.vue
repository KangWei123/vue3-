<template>
<div class="grandSon">

  孙子组件{{money}}
  <button @click="handleClick">money--</button>
</div>
</template>

<script>
import {inject} from 'vue'
import {contextMoney,handleContextMoney} from '../App.vue'
export default {
  setup(){
    const money = inject(contextMoney)
    const handleMoney = inject(handleContextMoney)

    const handleClick = ()=>{
      handleMoney(money.value - 1)
    }
    return {
      money,
      handleClick
    }
  }
}
</script>

<style>
.grandSon{
    border: 1px black solid;
    padding: 15px;
}
</style>