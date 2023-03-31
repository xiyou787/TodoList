<template>
  <section class="todoapp">
    <!-- 除了驼峰, 还可以使用-转换链接 -->
    <TodoHeader @addTodo="addTodo"></TodoHeader>
    <TodoMain
      :list="showList"
      @changeIsDone="changeIsDone"
      @delTodo="delTodo"
      @checkAll="checkAll"
    ></TodoMain>
    <TodoFooter
      :type="type"
      :list="list"
      @clearAll="clearAll"
      @isType="isType"
    ></TodoFooter>
  </section>
</template>

<script>
// 1.0 样式引入
import "./styles/base.css";
import "./styles/index.css";

import TodoHeader from "./components/TodoHeader";
import TodoMain from "./components/TodoMain";
import TodoFooter from "./components/TodoFooter";

export default {
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  data() {
    return {
      type: "all",
      list: JSON.parse(localStorage.getItem("todo")) || [
        { id: 100, name: "吃饭", isDone: true },
        { id: 201, name: "睡觉", isDone: false },
        { id: 103, name: "打豆豆", isDone: true },
      ],
    };
  },
  methods: {
    changeIsDone(id) {
      let goods = this.list.find((item) => item.id === id);
      goods.isDone = !goods.isDone;
    },
    delTodo(delId) {
      this.list = this.list.filter((item) => item.id != delId);
    },
    addTodo(todoName) {
      this.list.push({
        id: +new Date(),
        name: todoName,
        isDone: false,
      });
    },
    clearAll() {
      this.list = this.list.filter((item) => item.isDone === false);
    },
    isType(type) {
      this.type = type;
    },
    checkAll(value) {
      this.list.forEach((item) => (item.isDone = value));
    },
  },
  computed: {
    showList() {
      if (this.type === "ing") {
        return this.list.filter((item) => item.isDone === false);
      } else if (this.type === "ok") {
        return this.list.filter((item) => item.isDone === true);
      } else {
        return this.list;
      }
    },
  },
  watch: {
    list: {
      deep: true,
      handler(newVal) {
        localStorage.setItem("todo", JSON.stringify(newVal));
      },
    },
  },
};
</script>