<template>
  <header class="header">
    <h1>todos</h1>
    <input
      @keyup.enter="add"
      v-model="todoName"
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
    />
  </header>
</template>

<script>
export default {
  data() {
    return {
      todoName: "",
    };
  },
  methods: {
    add() {
      this.$emit("addTodo", this.todoName);
      this.todoName = "";
    },
  },
};
</script>