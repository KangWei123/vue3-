<template>
    <div>
        <h3>当前鼠标的位置</h3>
        <div>x:{{x}} -- y:{{y}}</div>
    </div>
</template>
<script>
import {onMounted,reactive,onBeforeUnmount,toRefs,toRef} from 'vue'
// composition API 可以实现逻辑的提取
const mousePosition = (unit)=>{
    const mouse = reactive({x:0,y:0})
    const mousemove = (e)=>{
        mouse.x = e.pageX +unit
        mouse.y = e.pageY +unit
    }
    onMounted(()=>document.addEventListener("mousemove",mousemove))
    onBeforeUnmount(() =>document.removeEventListener("mousemove",mousemove))
    return mouse
}
export default {
    setup(){
        console.log('setup')
        const mouse = mousePosition('px')
        return {
            // 展开数据
            ...toRefs(mouse)
        }
    }
}
</script>
<style scoped>

</style>