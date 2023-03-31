<template>
  <section class="main">
    <!-- 全选反选按钮 -->
    <input
      v-model="clickAll"
      id="toggle-all"
      class="toggle-all"
      type="checkbox"
    />
    <label for="toggle-all">Mark all as complete</label>
    <ul class="todo-list">
      <!-- 当任务已完成，可以给 li 加上 completed 类，会让元素加上删除线 -->
      <li
        v-for="item in list"
        :key="item.id"
        :class="{ completed: item.isDone }"
      >
        <div class="view">
          <!-- 如果是我的话  我就这么写 -->
          <!-- <input class="toggle" v-model="item.isDone" type="checkbox"/> -->
          <input
            :checked="item.isDone"
            @change="changeIsDone(item.id)"
            class="toggle"
            type="checkbox"
          />
          <label>{{ item.name }}</label>
          <button class="destroy" @click="del(item.id)"></button>
        </div>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  props: ["list"],
  methods: {
    changeIsDone(id) {
      this.$emit("changeIsDone", id);
    },
    del(delId) {
      this.$emit("delTodo", delId);
    },
  },
  computed: {
    clickAll: {
      get() {
        return this.list.every((item) => item.isDone === true);
      },
      set(val) {
        this.$emit("checkAll", val);
      },
    },
  },
};
</script>