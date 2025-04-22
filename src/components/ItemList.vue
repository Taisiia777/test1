<template>
    <div class="items-container">
      <div 
        v-for="item in items" 
        :key="item.id" 
        class="item" 
        :class="{ 'selected': isItemSelected(item) }"
        @click="handleItemClick(item)"
      >
        {{ item.name }}
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ItemList',
    props: {
      items: {
        type: Array,
        required: true
      },
      selectedItems: {
        type: Array,
        default: () => []
      },
      selectedItem: {
        type: Object,
        default: null
      },
      maxItems: {
        type: Number,
        required: true
      }
    },
    emits: ['toggle-item', 'select-item'],
    setup(props, { emit }) {
      const isItemSelected = (item) => {
        if (props.maxItems === 1) {
          return props.selectedItem && props.selectedItem.id === item.id;
        } else {
          return props.selectedItems.some(selectedItem => selectedItem.id === item.id);
        }
      };
      
      const handleItemClick = (item) => {
        if (props.maxItems === 1) {
          emit('select-item', item);
        } else {
          emit('toggle-item', item);
        }
      };
      
      return {
        isItemSelected,
        handleItemClick
      };
    }
  }
  </script>
  
  <style scoped>
  .items-container {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
  }
  
  .item {
    border: 2px solid #000;
    padding: 10px;
    text-align: center;
    cursor: pointer;
  }
  
  .item.selected {
    background-color: #f0f0f0;
  }
  </style>