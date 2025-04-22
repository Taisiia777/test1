<template>
  <div class="container">
    <!-- Верхний ряд -->
    <div class="box top-left">
      <SelectedUserItems :items="selectedUserItems" />
      <div class="status">selected: {{ selectedUserItems.length }} / 6</div>
    </div>
    
    <div class="box top-right">
      <SelectedChoiceItem :item="selectedChoiceItem" />
    </div>
    
    <!-- Нижний ряд -->
    <div class="box bottom-left">
      <ItemList 
        :items="userItems" 
        :selectedItems="selectedUserItems" 
        :maxItems="6"
        @toggle-item="toggleUserItem" 
      />
    </div>
    
    <div class="box bottom-right">
      <ItemList 
        :items="choiceItems" 
        :selectedItem="selectedChoiceItem" 
        :maxItems="1"
        @select-item="selectChoiceItem" 
      />
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import ItemList from './components/ItemList.vue';
import SelectedUserItems from './components/SelectedUserItems.vue';
import SelectedChoiceItem from './components/SelectedChoiceItem.vue';

export default {
  name: 'App',
  components: {
    ItemList,
    SelectedUserItems,
    SelectedChoiceItem
  },
  setup() {
    // Данные для левой нижней секции (вещи у пользователя)
    const userItems = ref([
      { id: 1, name: "Shoes 1" },
      { id: 2, name: "Shoes 2" },
      { id: 3, name: "Shoes 3" },
      { id: 4, name: "Shoes 4" },
      { id: 5, name: "T-shirt 1" },
      { id: 6, name: "T-shirt 2" },
      { id: 7, name: "T-shirt 3" },
      { id: 8, name: "T-shirt 4" }
    ]);
    
    // Данные для правой нижней секции (вещи на выбор)
    const choiceItems = ref([
      { id: 11, name: "Jacket 1" },
      { id: 12, name: "Jacket 2" },
      { id: 13, name: "Jacket 3" },
      { id: 14, name: "Jacket 4" },
      { id: 15, name: "Hoodie 1" },
      { id: 16, name: "Hoodie 2" },
      { id: 17, name: "Hoodie 3" },
      { id: 18, name: "Hoodie 4" }
    ]);
    
    // Выбранные предметы
    const selectedUserItems = ref([]);
    const selectedChoiceItem = ref(null);
    
    // Переключение выбора предмета пользователя (макс. 6)
    const toggleUserItem = (item) => {
      const index = selectedUserItems.value.findIndex(i => i.id === item.id);
      
      if (index !== -1) {
        // Удаляем предмет, если он уже выбран
        selectedUserItems.value.splice(index, 1);
      } else if (selectedUserItems.value.length < 6) {
        // Добавляем предмет, если выбрано меньше 6
        selectedUserItems.value.push(item);
      }
    };
    
    // Выбор предмета выбора (только 1 одновременно)
    const selectChoiceItem = (item) => {
      if (selectedChoiceItem.value && selectedChoiceItem.value.id === item.id) {
        // Отменяем выбор, если нажали на тот же предмет
        selectedChoiceItem.value = null;
      } else {
        // Выбираем новый предмет
        selectedChoiceItem.value = item;
      }
    };
    
    return {
      userItems,
      choiceItems,
      selectedUserItems,
      selectedChoiceItem,
      toggleUserItem,
      selectChoiceItem
    };
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, sans-serif;
  padding: 20px;
}

.container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: auto 1fr;
  gap: 20px;
  height: 100vh;
}

.box {
  border: 2px solid #000;
  padding: 10px;
}

.status {
  margin-top: 10px;
}
</style>