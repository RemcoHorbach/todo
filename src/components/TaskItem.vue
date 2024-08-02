<template>
    <li>
      <span :style="{ textDecoration: task.completed ? 'line-through' : 'none' }">
        {{ task.text }}
      </span>
      <button @click="toggleComplete">Complete</button>
      <button @click="editing = !editing">Edit</button>
      <input v-if="editing" v-model="newText" @keyup.enter="saveEdit" />
    </li>
  </template>
  
  <script>
  export default {
    name: 'TaskItem',
    props: {
      task: Object
    },
    data() {
      return {
        editing: false,
        newText: this.task.text
      };
    },
    methods: {
      toggleComplete() {
        this.$emit('toggle-complete');
      },
      saveEdit() {
        this.$emit('edit-task', this.newText);
        this.editing = false;
      }
    }
  };
  </script>
  
  <style>
  </style>