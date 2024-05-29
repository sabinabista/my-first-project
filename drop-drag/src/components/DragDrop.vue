<!-- <template>
    <div>
      <div
        class="drag-container"
        @dragover.prevent
        @drop="drop($event, 'list1')"
      >
        <h2>List 1</h2>
        <div
          class="drag-item"
          v-for="(item, index) in list1"
          :key="index"
          draggable="true"
          @dragstart="dragStart($event, 'list1', index)"
        >
          {{ item }}

        </div>
      </div>
      <div
        class="drag-container"
        @dragover.prevent
        @drop="drop($event, 'list2')"
      >
        <h2>List 2</h2>
        <div
          class="drag-item"
          v-for="(item, index) in list2"
          :key="index"
          draggable="true"
          @dragstart="dragStart($event, 'list2', index)"
        >
          {{ item }}
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    name: 'DragDrop',
    setup() {
      const list1 = ref(['Item 1', 'Item 2', 'Item 3']);
      const list2 = ref([]);
  
      const dragStart = (event, listName, index) => {
        event.dataTransfer.setData('text/plain', `${listName}-${index}`);
      };
  
      const drop = (event, targetList) => {
        const data = event.dataTransfer.getData('text/plain').split('-');
        const [sourceList, index] = data;
        const item = sourceList === 'list1' ? list1.value[index] : list2.value[index];
        if (sourceList !== targetList) {
          if (sourceList === 'list1') {
            list1.value.splice(index, 1);
          } else {
            list2.value.splice(index, 1);
          }
          list2.value.splice(index, 0, item);
        }
      };
  
      return {
        list1,
        list2,
        dragStart,
        drop,
      };
    },
  };
  </script>
  
  <style scoped>
  .drag-container {
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 10px;
    margin-bottom: 20px;
  }
  
  .drag-item {
    background-color: #f4f4f4;
    padding: 8px;
    margin-bottom: 5px;
    cursor: move;
  }
  </style>
   -->