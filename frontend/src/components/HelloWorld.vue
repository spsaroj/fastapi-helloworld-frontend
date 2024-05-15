<template>
  <div class="input-container">
    <input class="input-box" type="text" placeholder="task" v-model="taskName" @keyup.enter="addTodo">
    <input class="input-box" type="text" placeholder="description" v-model="taskDescription" @keyup.enter="addTodo">
    <button class="add-btn" @click="addTodo">Add Task</button>
    

  <div v-if="loading">Loading...</div>
    <div v-else>
      <ul>
        <li v-for="item in items" :key="item.id">
          <div class="taskContainer">
          {{ item.task_name }}<br/>
          </div>
          <div class="taskContainer">
          {{ item.task_description }}<br/>
          </div>
          <button class="delete-btn" @click="deleteTodo(item.id)">Delete</button>
          <button class="add-btn" @click="updateClicked(item.id)">Update</button>
          <br/><br/>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  data() {
    return {
      taskName: '',
      taskDescription:'',
      loading: true,
      items: []
    };
  },
  mounted() {
    this.fetchTasks();
  },
  methods: {
    async addTodo() {
      if (this.taskName.trim() !== '') {
        try {
        const rawData = {
          task_name: this.taskName,
          task_description: this.taskDescription
        };

        const response = await fetch('http://127.0.0.1:8000/tasks', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(rawData)
        });

        if (!response.ok) {
          throw new Error('Failed to submit task');
        }
        await this.fetchTasks();
        // Optionally, handle successful response
        console.log('Task submitted successfully');

        // Clear input fields
        this.taskName = '';
        this.taskDescription = '';
      } catch (error) {
        console.error('Error submitting task:', error);
      }
      };
    },

    updateClicked(taskId){
      this.$router.push({ path: '/update', query: { taskId } });
    },

    async deleteTodo(index) {
      try {
        const response = await fetch(`http://localhost:8000/tasks/${index}`, {
          method: 'DELETE'
        });

        if (!response.ok) {
          throw new Error('Failed to delete task');
        }
        await this.fetchTasks();
        // Optionally, handle successful response
        console.log('Task deleted successfully');
      } catch (error) {
        console.error('Error deleting task:', error);
      }
    },

    async fetchTasks() {
      try {
        const response = await fetch('http://127.0.0.1:8000/tasks/');
        if (!response.ok) {
          throw new Error('Failed to fetch tasks');
        }
        const data = await response.json();
        this.items = data;
        this.loading = false;
      } catch (error) {
        console.error('Error fetching tasks:', error);
      }
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .taskContainer{
    margin: 5px;
  }
</style>
