<template>
  <footer class="footer">
    <span class="todo-count">剩余<strong>{{total}}</strong></span>
    <ul class="filters"
        @click="changeType">
      <li>
        <a :class="{selected:isSel ==='all'}"
           @click="isSel = 'all'"
           href="javascript:;">全部</a>
      </li>
      <li>
        <a :class="{selected:isSel ==='no'}"
           @click="isSel = 'no'"
           href="javascript:;">未完成</a>
      </li>
      <li>
        <a :class="{selected:isSel ==='yes'}"
           @click="isSel = 'yes'"
           href="javascript:;">已完成</a>
      </li>
    </ul>
    <button class="clear-completed"
            @click="delDone">清除已完成</button>
  </footer>
</template>

<script>
export default {
  props: ['list'],
  data () {
    return {
      isSel: 'all',    // yer   no
    }
  },
  computed: {
    total () {
      return this.list.length
    }
  },
  methods: {
    changeType () {
      this.$emit('changeType', this.isSel)
    },
    delDone () {
      this.$emit('delDone')
    }
  }
}
</script>