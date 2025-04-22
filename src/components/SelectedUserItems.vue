<template>
    <div class="selected-items">
      <div v-for="item in items" :key="item.id" class="selected-item">
        {{ item.name }}
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'SelectedUserItems',
    props: {
      items: {
        type: Array,
        required: true
      }
    }
  }
  </script>
  
  <style scoped>
  .selected-items {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
  }
  
  .selected-item {
    border: 2px solid #000;
    padding: 10px;
    text-align: center;
  }
  </style>