<!-- src/components/UpdateView.vue -->
<template>
    <div>
      <input class="input-box" v-model="updatedTaskTitle" placeholder="Task Title" />
      <input class="input-box" v-model="updatedTaskDescription" placeholder="Task Description" />
      <button class="add-btn" @click="updateTask">Update Task</button>
      <button class="back-btn" @click="backToHome">Back to Home</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      taskId: {
        type: Number,
        required: true
      }
    },
    data() {
      return {
        updatedTaskTitle: '',
        updatedTaskDescription: ''
      };
    },
    mounted() {
      this.fetchTask();
    },
    methods: {
      async fetchTask() {
        try {
          const response = await fetch(`http://localhost:8000/tasks/${this.taskId}`, {
            method: 'GET',
            headers: {
              'Content-Type': 'application/json'
            }
          });
  
          if (!response.ok) {
            if (response.status === 404) {
              throw new Error('Task not found');
            }
            throw new Error('Failed to fetch task');
          }
  
          const data = await response.json();
          this.updatedTaskTitle = data.task_name;
          this.updatedTaskDescription = data.task_description;
        } catch (error) {
          this.task = null; // Clear any previous task data
          console.error('Error fetching task:', error.message);
        }
      },
      async updateTask() {
        try {
          const response = await fetch(`http://localhost:8000/tasks/${this.taskId}`, {
            method: 'PUT',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify({
              task_name: this.updatedTaskTitle,
              task_description: this.updatedTaskDescription
            })
          });
  
          if (!response.ok) {
            throw new Error('Failed to update task');
          }
  
          console.log('Task updated successfully');
          this.backToHome();
        } catch (error) {
          console.error('Error updating task:', error);
        }
      },
      backToHome() {
        this.$router.push('/');
      }
    }
  };
  </script>
  