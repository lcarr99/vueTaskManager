<template>
  <div class="addTask ">
    <div class="container">
      <div class="row">
        <div class="col-lg-12">
          <form action="">
            <div class="form-group">
              <label for="title">Title</label>
              <input type="text" v-model="title" name="title" class="form-control form-control-sm" id="title" aria-describedby="emailHelp" placeholder="Enter Title">
            </div>
            <div class="form-group">
              <label for="Description">Description</label>
              <textarea name="description" v-model="description" class="form-control" id="description" placeholder="Description">
              </textarea>
            </div>
          </form>
          <div class="btn btn-primary" v-on:click="addTask()">Submit</div>
        </div>
      </div>
      <br>
    </div>
  </div>

</template>

<script>
import axios from 'axios'
export default {
  name: 'addTask',
  components: {
    axios
  },
  props: ['tasks'],
  data: function () {
    return {
      title: '',
      description: ''
    }
  },
  methods: {
    addTask () {
      axios.post('http://localhost:3000/tasks', {'title': this.title, 'description': this.description, 'completed': false})
        .then(res => {
          this.tasks.push(res.data)
          this.title = ''
          this.description = ''
        })
    }
  }
}
</script>

<style scoped>
  input[type=text]{
    width: 500px;
  }
  textarea{
    width: 500px;
  }
</style>
