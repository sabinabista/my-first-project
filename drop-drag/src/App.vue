
  <template>
    <div class="flex pt-3">
  <div class="w-1/5 mx-auto">
    <h1 class="font-bold text-3xl text-center pb-2.5">Box 1</h1>
    <div class=" drop-zone bg-purple-300 p-8 min-h-52  "
        @drop.prevent="onDrop($event, 1)"
        @dragenter.prevent
        @dragover.prevent
      >
        <div  v-for="item in getList(1)"
          :key="item.id"
          class="drag-el mb-2.5 p-2.5 font-bold  last:mb-0 bg-purple-500 text-white"
          draggable="true"
          @dragstart="startDrag($event,item)"
        >
          {{ item.title }}
        </div>
      </div> 
  </div>
  <div class="w-1/5 mx-auto">
  <h1 class="font-bold text-3xl text-center pb-2.5">Box 2</h1>
      <div class="drop-zone bg-purple-300 p-8 min-h-52 "
        @drop.prevent="onDrop($event, 2)"
        @dragenter.prevent
        @dragover.prevent
      >
        <div v-for="item in getList(2)"
          :key="item.id"
          class="drag-el mb-2.5 p-2.5 font-bold last:mb-0 bg-purple-500 text-white"
          draggable="true"
          @dragstart="startDrag($event,item)"
        >
          {{ item.title }}
        </div>
      </div>
      </div>
    </div>
{{ form.name   }}
{{ array[1] }}
    <form>
      <input placeholder="name" v-model="form.name"/>
    </form>
  </template>
  
  <script setup>
  import { ref } from 'vue'

const array = ['name','email']

  const form = ref({
    name:''
  })

      const items = ref([
        { id: 0, title: 'Item A', List: 1 },
        { id: 1, title: 'Item B', List: 1 },
        { id: 2, title: 'Item C', List: 1 },
      ])
  
      const getList = (List) => {
        return items.value.filter((item) => item.List === List)
      }
  
      const startDrag = (event, item) => {
        event.dataTransfer.effectAllowed = 'move'
        event.dataTransfer.setData('itemID', item.id)
      }
  
      const onDrop = (event, List) => {
        const itemID = event.dataTransfer.getData('itemID')
        const item = items.value.find((item) => item.id == parseInt(itemID))
        if (item) {
          // Remove item from its current list
          items.value = items.value.filter((i) => i.id !== item.id)
          // Calculate the drop index
          const dropZone = event.currentTarget
          const dropZoneRect = dropZone.getBoundingClientRect()
          const dropY = event.clientY - dropZoneRect.top
          const targetList = getList(List)
          let insertIndex = targetList.length
          for (let i = 0; i < targetList.length; i++) {
            const targetItem = dropZone.children[i]
            const targetRect = targetItem.getBoundingClientRect()
            if (dropY < targetRect.top + targetRect.height / 2) {
              insertIndex = i
              break
            }
          }
          // Insert item at the calculated position in the new list
          items.value.splice(insertIndex, 0, { ...item, List })
        }
      }
  
     
  </script>
  
  <style>
  /* .drop-zone {
    width: 20%;
    margin: 20px auto;
    background-color: rgb(221, 179, 245);
    padding: 30px;
    min-height: 10px;
   
 
    

  } */
  /* .main-items{
    display: flex;
    align-items: center;
gap: 50px;   

  } */

  /* .drag-el{
    padding-bottom: 20px;
    font-weight: bold;
  }  */
  </style>
  
        
  

 