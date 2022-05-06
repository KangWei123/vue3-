// watch 的使用
<template>
  watch
  <p>我的存款{{ money }}</p>
  <p>车{{ car.branch }} --{{ car.price }}</p>
  <p>count{{ count }}</p>
  <button @click="money++">money++</button>
  <button @click="car.price++">price++</button>
  <button @click="count++">count++</button>
</template>

<script>
import { computed, readonly, reactive, ref, watch, toRefs } from "vue";
export default {
  setup() {
    const state = reactive({
      money: 100,
      car: {
        branch: "宝马",
        price: 1000,
      },
    });
    const count = ref(100);
    const msg = ref('msg');
    // 接收3个参数
    // 参数1：监视的数据源 可以是一个ref 或者是一个函数等...
    // 参数2：回调函数 (value, oldValue) =>{}
    // 参数3：额外的配置 是一个对象 { deep: true, immediate: true }

    // 1 侦听单个数据源
    // 1.1 侦听器一个拥有返回值的 getter 函数
    watch(
      () => state.money,
      (money, prevMoney) => {
        console.log(`money变化了，新值${money},旧值${prevMoney}`);
      }
    );
    // 直接侦听一个 ref 
    let watchC = watch(count, (val, oldVal) => {
      console.log(`count变化了，新值${val},旧值${oldVal}`);
    });
    // 监听ref所定义的多个响应式数据
    watch([count,msg], (val, oldVal) => {
      console.log(val, oldVal);
      // console.log(`${val}-${oldVal}`);
      // console.log(`999count变化了，新值${val},旧值${oldVal}`);
    });

    // 也可以直接侦听reactive 注意此处无法获得oldvalue
    watch(
      state,
      (val, oldVal) => {
        console.log('state', val.money, oldVal&&oldVal.money);
        // console.log(1111,JSON.stringify(val),JSON.stringify(oldVal),)
      },
      {
        deep: true,
        immediate: true,
      }
    );

    // 侦听多个数据源
    // watch([()=>state.money,()=>state.car.price],([money,prevMoney],[price,prevPrice])=>{
    //   console.log('222数据变化了', money,price)
    // })

    // 调用watchC 用于清掉侦听器
    // console.log(88,watchC)
    return {
      ...toRefs(state),
      count,
      msg
    };
  },
};
</script>

<style></style>
