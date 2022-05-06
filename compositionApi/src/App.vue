// provide 和 inject
<template>
  <div class="father">
    <div>
      父组件{{ money }}
      <button @click="money++">money++</button>
    </div>
    <Son></Son>
    <!-- 鼠标位置 -->
    <!-- <MousePosition></MousePosition>
    <UseSetup></UseSetup>
    <UseReactive></UseReactive>
    <UseReadonly/>
    <UseRef></UseRef> -->
    <UseComputed/>
    <UseWatch/>
    <LifeCycle/>
  </div>
</template>
<script>
import { ref, provide } from "vue";
import MousePosition from "./components/mousePosition.vue";
import Son from "./components/son.vue";
import UseSetup from "./components/useSetup.vue";
import UseReactive from "./components/useReactive.vue";
import UseRef from "./components/useRef.vue";
import UseReadonly from "./components/useReadonly.vue";
import UseComputed from "./components/useComputed.vue";
import UseWatch from "./components/useWatch.vue";
import LifeCycle from "./components/lifeCycle.vue";
export const contextMoney = Symbol("money");
export const handleContextMoney = Symbol("handleMoney");
export default {
  components: {
    Son,
    MousePosition,
    UseSetup,
    UseReactive,
    UseRef,
    UseReadonly,
    UseComputed,
    UseWatch,
    LifeCycle,
  },
  setup() {
    const money = ref(101);
    // 提供数据
    provide(contextMoney, money);
    // 提过修改数据的方法
    provide(handleContextMoney, (value) => {
      money.value = value;
    });
    return {
      money,
    };
  },
};
</script>
<style>
.father {
  /* width: 100vw; */
  /* height: 200px; */
  padding: 15px;
  border: 1px black solid;
}
</style>
