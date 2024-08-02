<template>
  <div id="app">
    <h1>Vue To-Do List</h1>
    <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task" />
    <button @click="addTask">Add Task</button>
    <TaskList :tasks="tasks" @edit-task="editTask" @toggle-complete="toggleComplete" />
  </div>
</template>

<script>
import TaskList from './components/TaskList.vue';

export default {
  name: 'App',
  components: {
    TaskList
  },
  data() {
    return {
      newTask: '',
      tasks: JSON.parse(localStorage.getItem('tasks')) || []
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.tasks.push({ text: this.newTask, completed: false });
        this.newTask = '';
        this.saveTasks();
      }
    },
    editTask(index, newText) {
      this.tasks[index].text = newText;
      this.saveTasks();
    },
    toggleComplete(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
      this.saveTasks();
    },
    saveTasks() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    }
  }
};
</script>

<style>

</style>