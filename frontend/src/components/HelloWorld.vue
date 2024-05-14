<template>
  <div>
    <input type="text" v-model="newTodo" @keyup.enter="addTodo">
    <button @click="addTodo">Add Task</button>
    

  <div v-if="loading">Loading...</div>
    <div v-else>
      <ul>
        <li v-for="item in items" :key="item.id">
          {{ item.task_name }}
          <button @click="deleteTodo(index)">Delete</button></li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'HelloWorld',
  data() {
    return {
      newTodo: '',
      loading: true,
      items: []
    };
  },
  mounted() {
        axios.get('http://127.0.0.1:8080/tasks/')
        .then(response=>(this.item = response))
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({ text: this.newTodo });
        this.newTodo = '';
      }
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
