<template>
  <div>
    <header>
      my Trello
    </header>
    <main>
      <p class="info-line">All: {{totalCardCount}} tasks</p><!--/.info-line-->
        <draggable 
          :list="lists" 
          class="list-index"
          @end="movingList"
        >
        <list
          v-for="(item,index) in lists"
          :key="item.id"
          :title="item.title"
          :listIndex="index"
          :cards="item.cards"
          @change="movingCard"
        />
        <ListAdd/>
      </draggable><!--/.list-index-->
    </main>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
import ListAdd from './ListAdd.vue'
import List from './List.vue'
import {mapState} from 'vuex'
export default{
  components:{
    ListAdd,
    List,
    draggable
  },
  computed:{
    ...mapState([
    'lists'
    ]),
    totalCardCount(){
      return this.$store.getters.totalCardCount
    }
  },
  methods:{
    movingCard:function(){
      this.$store.dispatch('updateList',{lists:this.lists})
    },
    movingList:function(){
      this.$store.dispatch('updateList',{lists:this.lists})
    }
  }
}
</script>