<template>
  <footer class="footer" v-if="list.length">
    <span class="todo-count"
      >剩余<strong>数量值{{ okNum }}</strong></span
    >
    <ul class="filters">
      <li>
        <a
          @click="filter('all')"
          :class="{ selected: type === 'all' }"
          href="javascript:;"
          >全部</a
        >
      </li>
      <li>
        <a
          @click="filter('ing')"
          :class="{ selected: type === 'ing' }"
          href="javascript:;"
          >未完成</a
        >
      </li>
      <li>
        <a
          @click="filter('ok')"
          :class="{ selected: type === 'ok' }"
          href="javascript:;"
          >已完成</a
        >
      </li>
    </ul>
    <button v-show="ClearAll" class="clear-completed" @click="clear">
      清除已完成
    </button>
  </footer>
</template>

<script>
export default {
  props: ["list", "type"],
  methods: {
    clear() {
      this.$emit("clearAll");
    },
    filter(type) {
      this.$emit("isType", type);
    },
  },
  computed: {
    okNum() {
      return this.list.filter((item) => item.isDone === false).length;
    },
    ClearAll() {
      return this.list.some((item) => item.isDone === true);
    },
  },
};
</script>