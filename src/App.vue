<template>
  <div id="app">
    <Header />
    <div class="board">
      <div class="drop-zone"
      @drop="onDrop($event, 1)"
      @dragover.prevent
      @dragenter.prevent>
        <div class="lane">
          <h2 class="lane-title">To do</h2>
          <Card v-for="item in listOne"
          :key="item.title"
          class="drag-el"
          draggable="true"
          @dragstart="startDrag($event, item)">
            {{ item.title }}
          </Card>
        </div>
      </div>
      <div class="drop-zone"
      @drop="onDrop($event, 2)"
      @dragover.prevent
      @dragenter.prevent>
        <div class="lane">
            <h2 class="lane-title">Doing</h2>
            <Card
            v-for="item in listTwo"
            :key="item.title"
            class="drag-el"
            draggable="true"
            @dragstart="startDrag($event, item)">
              {{ item.title }}
            </Card>
        </div>
      </div>
      <div class="drop-zone"
      @drop="onDrop($event, 3)"
      @dragover.prevent
      @dragenter.prevent>
        <div class="lane">
            <h2 class="lane-title">Done</h2>
            <Card v-for="item in listThree"
            :key="item.title"
            class="drag-el"
            draggable="true"
            @dragstart="startDrag($event, item)">
              {{ item.title }}
            </Card>
        </div>
      </div>
    </div>
  </div>
</template>


<script>


import Header from './components/Header';
import Card from './components/Card';




export default {
  name: 'App',
  components: {
    Header,
    Card
  },
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
          list: 2,
        },
        {
          id: 3,
          title: 'Item D',
          list: 3,
        },
      ],
    }
  },
  computed: {
    listOne() {
      return this.items.filter((item) => item.list === 1)
    },
    listTwo() {
      return this. items.filter((item) => item.list === 2)
    },
    listThree() {
      return this.items.filter((item) => item.list === 3)
    }
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
    }
  }
}
</script>


<style>
.board{
  display: flex;
  margin: 1.2rem .8rem;
  align-items: flex-start;
}


.lane{
  background: var(--color-grey);
  width: 23rem;
  border-radius: .8rem;
  box-shadow: 0 .1rem .2rem 0 rgba(33, 33, 33, 0.1);
  padding: 0 .7rem;
  margin: 0 .8rem
}


.lane-title{
  padding: .8rem .5rem;
  margin-bottom: .6rem;
}


.placeholder {
  background: rgba(33, 33, 33, .08);
  border-radius: .4rem;
  transform: scaleY(0.85);
  transform-origin: 0% 0%;
}


</style>
