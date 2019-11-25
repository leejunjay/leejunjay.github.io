<template>
  <div id="app">
    <todolist/>
  </div>
</template>

<script>
import todolist from './components/todolist'

export default {
  name: 'App',
  components: {
    todolist
  }
}
</script>

<style>
  * {
    padding: 0;
    margin: 0 auto;
  }
  body {
    padding: 10px;
  }
</style>
