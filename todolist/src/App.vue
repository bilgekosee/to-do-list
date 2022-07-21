<template>

<div id="app">
  <todolist></todolist>
</div>
   
</template>

<script>
import todolist from './components/todolist.vue'

export default {
  name: 'App',
  components: {
    // eslint-disable-next-line vue/no-unused-components
    todolist
  }
}
</script>
