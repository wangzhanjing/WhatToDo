<template>
  <div>
    <section class="todoapp">
      <!-- 除了驼峰, 还可以使用-转换链接 -->
      <todoHeader :list="showArr"
                  @add="addItem"></todoHeader>
      <todoMain :list="showArr"
                @del="del"></todoMain>
      <todoFoot :list="showArr"
                @changeType="changeType"
                @delDone="delDone"></todoFoot>
    </section>
  </div>
</template>

<script>
// 1.0 样式引入
import "./styles/base.css"
import "./styles/index.css"

import todoHeader from "./components/todoHeader";
import todoMain from "./components/todoMain";
import todoFoot from "./components/todoFoot";


export default {
  components: {
    todoHeader,
    todoMain,
    todoFoot,
  },
  data () {
    return {
      list: JSON.parse(localStorage.getItem('todoList')) || [],
      getSel: 'all'
    }
  },
  computed: {
    showArr () {
      if (this.getSel === 'yes') {
        return this.list.filter(item => item.isDone === true)
      } else if (this.getSel === 'no') {
        return this.list.filter(item => item.isDone === false)
      } else {
        return this.list
      }
    }
  },
  watch: {
    list: {
      deep: true,
      handler () {
        localStorage.setItem('todoList', JSON.stringify(this.list))
      }
    }
  },
  methods: {
    addItem (name) {
      let item = {
        id: this.list.length,
        name: name,
        isDone: false
      }
      this.list.push(item)
    },
    del (id) {
      let index = this.list.findIndex(item => {
        return item.id === id
      })
      this.list.splice(index, 1)
    },
    changeType (type) {
      this.getSel = type
    },
    delDone () {
      this.list = this.list.filter(item => item.isDone === false)
    }
  }
};
</script>