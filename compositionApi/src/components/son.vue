<template>
  <div class="son">
      子组件{{money}}
  <GrandSon></GrandSon>
  </div>
</template>

<script>
import {inject} from 'vue'
import GrandSon from './grandSon.vue'
import { contextMoney } from '../App.vue'
export default {
    components:{GrandSon},
    setup(){
        const money = inject(contextMoney)
        return {
            money
        }
    }
}
</script>

<style>
.son{
    border: 1px black solid;
    padding: 15px;
}
</style>