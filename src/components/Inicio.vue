<template>
    <div>
        <div 
            class="drop-zone" 
            @drop="onDrop($event, 1)"
            @dragover.prevent
            @dragenter.prevent
        >
            <div 
                class="drag-el"
                v-for="item in listOne" 
                :key="item.title" 
                draggable
                @dragstart="startDrag($event, item)"
            >
                {{ item.title }}
            </div>
        </div>
    </div>

</template>

<script>

export default {
    data() {
        return {
            items: [
                {
                    id: 0,
                    title: 'Item A',
                    list: 1,
                },
                {
                    id: 1,
                    title: 'Item B',
                    list: 1,
                },
                {
                    id: 2,
                    title: 'Item C',
                    list: 1,
                },
            ],
        }
    },

    computed: {
        listOne() {
            return this.items.filter((item) => item.list === 1)
        },
    },

    methods: {
    startDrag(evt, item) {
      evt.dataTransfer.dropEffect = 'move'
      evt.dataTransfer.effectAllowed = 'move'
      evt.dataTransfer.setData('itemID', item.id)
    },
    onDrop(evt, list) {
      const itemID = evt.dataTransfer.getData('itemID')
      const item = this.items.find((item) => item.id == itemID)
      item.list = list
    },
  },

}

</script>


<style scoped>
.drop-zone {
  background-color: #eee;
  margin-bottom: 10px;
  padding: 10px;
  width: 50vw;
}
.drag-el {
  background-color: #fff;
  margin-bottom: 10px;
  padding: 10px;
  color: rgb(92, 91, 91);
}
</style>