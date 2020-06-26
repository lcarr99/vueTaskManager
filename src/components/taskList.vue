<template>

  <div class="container">
    <div class="row">
      <div class="col-lg-12">
        <table v-if="tasks.length !== 0" class="table">
          <tr>
            <th>Title</th>
            <th>Description</th>
            <th> </th>
          </tr>
          <tr  :key="task.id" v-for="task in tasks">
            <td>{{ task.title }}</td>
            <td>{{ task.description}}</td>
            <td><div v-on:click="completeTask(task)" class="btn btn-danger">Complete</div></td>
          </tr>
        </table>
      </div>
    </div>
  </div>

</template>

<script>
import axios from 'axios'
export default {
  name: 'taskList',
  components: {
    axios
  },
  props: ['tasks'],
  data: function () {
    return {edit: false}
  },

  methods: {
    completeTask (task) {
      let data = {'title': task.title, 'description': task.description, 'completed': true}
      let tasks = this.tasks
      axios.put('http://localhost:3000/tasks/' + task.id + '/', data).then(function () {
        tasks.splice(task, 1)
      })
    }
  }
}

</script>

<style scoped>

</style>
