<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" >
    <label for="toggle-all"></label> 
    <!-- label 可以关联一个表单标签 -->
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      v-model="task"
      @keydown.enter="enter"
      ref="input"
    />
  </header>
</template>

<script>
export default {
 data() {
    return {
        // property: {{'value'}},
        task:''
    };

 }, 
methods: {
    enter() {
        if (this.task.trim().length == 0) {
            this.task = "";
            return alert("Please enter a task");
        }
        this.$emit("add", this.task);
        this.task = "";
    },
},
computed: {
    isAll: {
        get() {
            return this.$parent.list.every((ele) => ele.isDone);
        },
        set(checked) {
            this.$parent.list.forEach((ele) => (ele.isDone = checked));
        },
    },
},
};
</script>