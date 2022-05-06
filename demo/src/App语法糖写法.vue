//语法糖写法
<template>
  <section class="todoapp">
    <header class="header">
      <h1>todos2</h1>
      <input
        class="new-todo"
        placeholder="What needs to be done?"
        autofocus
        @keyup.enter="keyupEnter"
        v-model="inputvalue"
      />
    </header>
    <!-- This section should be hidden by default and shown when there are todos -->
    <section class="main">
      <input
        id="toggle-all"
        class="toggle-all"
        type="checkbox"
        v-model="checkboxAll"
      />
      <label for="toggle-all">Mark all as complete</label>
      <ul class="todo-list">
        <!-- These are here just to show the structure of the list items -->
        <!-- List items should get the class `editing` when editing and `completed` when marked as completed -->
        <!-- <li class="completed">
						<div class="view">
							<input class="toggle" type="checkbox" checked>
							<label>Taste JavaScript</label>
							<button class="destroy"></button>
						</div>
						<input class="edit" value="Create a TodoMVC template">
					</li>
					<li >
						<div class="view">
							<input class="toggle" type="checkbox" >
							<label>Buy a unicorn</label>
							<button class="destroy"></button>
						</div>
						<input class="edit" value="Rule the web">
					</li> -->
        <!-- class="editing" -->
        <li
          @dblclick="dbclickItem(item.id, item.labelValue)"
          v-for="item in list"
          :key="item.id"
          :class="{
            completed: item.inputChecked,
            editing: currentEditingId === item.id,
          }"
        >
          <div class="view">
            <input class="toggle" type="checkbox" v-model="item.inputChecked" />
            <label>{{ item.labelValue }}</label>
            <button class="destroy" @click="delItem(index)"></button>
          </div>
          <input
            class="edit"
            v-model="item.labelValue"
            @keyup.enter="confirmEdit"
          />
        </li>
      </ul>
    </section>
    <!-- This footer should hidden by default and shown when there are todos -->
    <footer class="footer">
      <!-- This should be `0 items left` by default -->
      <span class="todo-count"
        ><strong>{{ total }}</strong> item left</span
      >
      <!-- Remove this if you don't implement routing -->
      <ul class="filters">
        <li>
          <a class="selected" href="#/">All</a>
        </li>
        <li>
          <a href="#/active">Active</a>
        </li>
        <li>
          <a href="#/completed">Completed</a>
        </li>
      </ul>
      <!-- Hidden if no completed items are left ↓ -->
      <button class="clear-completed" @click="delSelect">
        Clear completed
      </button>
    </footer>
  </section>
  {{ msg }}
  <Son ref="childRef" :title="title" @childFn="childFn"></Son>
</template>
<script setup>
// script setup>语法糖  无需return 无需注册组件
// script setup>语法糖里面的代码会被编译成组件 setup() 函数的内容，不需要通过return暴露
// 声明的变量、函数以及import引入的内容，即可在<template/>使用，并且不需要写export default{}
import {
  reactive,
  toRefs,
  computed,
  watch,
  ref,
  nextTick,
  onMounted,
} from "vue";
import Son from "./components/son.vue";
//注册响应数据
const childRef = ref();
onMounted(() => {
  //子组件接收暴露出来得值
  console.log("childRef", childRef.value.name);
  console.log(childRef.value.toEmits);
});

const msg = ref("我和我的祖国");
const title = ref("一刻也不能分割");
const state = reactive({
  list: [
    {
      inputChecked: true,
      labelValue: "unicorn",
      id: "0",
    },
    {
      inputChecked: false,
      labelValue: "JavaScript",
      id: "1",
    },
  ],
  currentEditingId: "",
  currentEditingName: "",
  inputvalue: "",
});
// 回车 确认
const keyupEnter = () => {
  state.list.unshift({
    inputChecked: false,
    labelValue: state.inputvalue,
    id: state.list.length,
  });
  // 清空inputvalue
  state.inputvalue = "";
};
// 子组件触发方法
const childFn = (val) => {
  // alert(val)
  title.value = val;
};
// 全选 全不选按钮
const selectAll = () => {
  let isTrue = state.list.every((item) => item.inputChecked);
  if (isTrue) {
    // 全部为选中  设置为不选中
    state.list.forEach((item) => (item.inputChecked = false));
  } else {
    // 设置为选中
    state.list.forEach((item) => (item.inputChecked = true));
  }
};
// 删除单个
const delItem = (id) => {
  state.list.splice(id, 1);
};
// 删除选中的
const delSelect = () => {
  state.list = state.list.filter((item) => !item.inputChecked);
};
// 双击编辑
const dbclickItem = (id, name) => {
  state.currentEditingId = id;
  state.currentEditingName = name;
};
// 修改完毕-回车
const confirmEdit = (id, name) => {
  state.currentEditingId = "";
  state.currentEditingName = "";
};
const total = computed(
  () => state.list.filter((item) => !item.inputChecked).length
);
const checkboxAll = computed({
  get() {
    return state.list.every((item) => item.inputChecked);
  },
  set(value) {
    selectAll();
  },
});
const { list, currentEditingId, currentEditingName, inputvalue } = {
  ...toRefs(state),
};
</script>
<style>
@import url("../public/index.css");
hr {
  margin: 20px 0;
  border: 0;
  border-top: 1px dashed #c5c5c5;
  border-bottom: 1px dashed #f7f7f7;
}

.learn a {
  font-weight: normal;
  text-decoration: none;
  color: #b83f45;
}

.learn a:hover {
  text-decoration: underline;
  color: #787e7e;
}

.learn h3,
.learn h4,
.learn h5 {
  margin: 10px 0;
  font-weight: 500;
  line-height: 1.2;
  color: #000;
}

.learn h3 {
  font-size: 24px;
}

.learn h4 {
  font-size: 18px;
}

.learn h5 {
  margin-bottom: 0;
  font-size: 14px;
}

.learn ul {
  padding: 0;
  margin: 0 0 30px 25px;
}

.learn li {
  line-height: 20px;
}

.learn p {
  font-size: 15px;
  font-weight: 300;
  line-height: 1.3;
  margin-top: 0;
  margin-bottom: 0;
}

#issue-count {
  display: none;
}

.quote {
  border: none;
  margin: 20px 0 60px 0;
}

.quote p {
  font-style: italic;
}

.quote p:before {
  content: "“";
  font-size: 50px;
  opacity: 0.15;
  position: absolute;
  top: -20px;
  left: 3px;
}

.quote p:after {
  content: "”";
  font-size: 50px;
  opacity: 0.15;
  position: absolute;
  bottom: -42px;
  right: 3px;
}

.quote footer {
  position: absolute;
  bottom: -40px;
  right: 0;
}

.quote footer img {
  border-radius: 3px;
}

.quote footer a {
  margin-left: 5px;
  vertical-align: middle;
}

.speech-bubble {
  position: relative;
  padding: 10px;
  background: rgba(0, 0, 0, 0.04);
  border-radius: 5px;
}

.speech-bubble:after {
  content: "";
  position: absolute;
  top: 100%;
  right: 30px;
  border: 13px solid transparent;
  border-top-color: rgba(0, 0, 0, 0.04);
}

.learn-bar > .learn {
  position: absolute;
  width: 272px;
  top: 8px;
  left: -300px;
  padding: 10px;
  border-radius: 5px;
  background-color: rgba(255, 255, 255, 0.6);
  transition-property: left;
  transition-duration: 500ms;
}

@media (min-width: 899px) {
  .learn-bar {
    width: auto;
    padding-left: 300px;
  }

  .learn-bar > .learn {
    left: 8px;
  }
}
</style>
