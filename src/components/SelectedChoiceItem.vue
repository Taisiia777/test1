<template>
    <div class="centered">
      <template v-if="item">
        SELECTED<br>ITEM<br><br>{{ item.name }}
      </template>
      <template v-else>
        SELECTED<br>ITEM
      </template>
    </div>
  </template>
  
  <script>
  export default {
    name: 'SelectedChoiceItem',
    props: {
      item: {
        type: Object,
        default: null
      }
    }
  }
  </script>
  
  <style scoped>
  .centered {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    font-weight: bold;
    text-align: center;
  }
  </style>
  
