<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all"
           class="toggle-all"
           type="checkbox"
           v-model="isAll">
    <label for="toggle-all"></label>
    <input class="new-todo"
           placeholder="输入任务名称-回车确认"
           autofocus
           v-model="listName"
           @keydown.enter="add" />
  </header>
</template>

<script>
export default {
  data () {
    return {
      listName: ''
    }
  },
  props: ['list'],
  computed: {
    isAll: {
      set (checked) {
        this.list.forEach(item => item.isDone = checked)
      },
      get () {
        return this.list.length !== 0 && this.list.every(item => item.isDone === true)
      }
    }
  },
  methods: {
    add () {
      this.$emit('add', this.listName)
      this.listName = ''
    }
  }
}
</script>