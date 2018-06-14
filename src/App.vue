<template>
  <div id="app">
    <ToDoList></ToDoList>
  </div>
</template>

<script>
import ToDoList from './components/ToDoList.vue';

export default {
  name: 'app',
  components: {
    ToDoList,
  }
}
</script>

<style>
</style>
