<template>
  <div id="app">
    <navigation logo="Liam's Tasks" />
    <addTask :tasks="this.tasks"/>
    <taskList :tasks="this.tasks" />
  </div>
</template>

<script>
import navigation from './components/header'
import addTask from './components/addTask'
import taskList from './components/taskList'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    navigation,
    addTask,
    taskList,
    axios
  },
  data: function () {
    return {
      tasks: []
    }
  },
  mounted () {
    axios.get('http://localhost:3000/tasks?completed=false').then(res => {
      this.tasks = res.data
    })
  }
}
</script>

<style>

</style>
