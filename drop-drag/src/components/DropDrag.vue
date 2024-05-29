<template>
  <draggable v-model="items" @end="onDragEnd">
    <div v-for="(item, index) in items" :key="index">{{ item }}</div>
  </draggable>
</template>

<script>
import { draggable } from 'vuedraggable'

export default {
  components: {
    draggable
  },
  data() {
    return {
      items: ['Item 1', 'Item 2', 'Item 3']
    }
  },
  methods: {
    onDragEnd(event) {
      console.log('Dragged item:', event.item)
    }
  }
}
</script>
