<template>
    <ul>
      <TaskItem
        v-for="(task, index) in tasks"
        :key="index"
        :task="task"
        @edit-task="editTask(index, $event)"
        @toggle-complete="toggleComplete(index)"
      />
    </ul>
  </template>
  
  <script>
  import TaskItem from './TaskItem.vue';
  
  export default {
    name: 'TaskList',
    components: {
      TaskItem
    },
    props: {
      tasks: Array
    },
    methods: {
      editTask(index, newText) {
        this.$emit('edit-task', index, newText);
      },
      toggleComplete(index) {
        this.$emit('toggle-complete', index);
      }
    }
  };
  </script>
  
  <style>
  </style>