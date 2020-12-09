<template>
    <div class="list">
        <div class="listheader">
            <p class="list-title">{{title}}</p>
            <p class="list-counter">total:{{totalCardInList}}</p><!--/.list-counter-->
            <div class="deletelist" @click="removeList">x</div><!--/.deletelist-->
        </div><!--/.listheader-->
        <draggable 
            group="cards" 
            :list="cards"
            @end="$emit('change')"
        >
            <Card 
                v-for="(item,index) in cards"
                :body="item.body"
                :key="item.id"
                :cardIndex="index"
                :listIndex="listIndex"
            />
            <CardAdd :listIndex="listIndex"/>
        </draggable>
    </div><!--/.list-->
</template>
    
<script>
    import draggable from 'vuedraggable'
    import CardAdd from './CardAdd.vue'
    import Card from './Card.vue'

    export default{
        components:{
            CardAdd,
            Card,
            draggable
        },
        props:{
            title:{
                type:String,
                required:true
            },
            listIndex:{
                type:Number,
                required:true
            },
            cards:{
                type:Array,
                required:true
            }
        },
        methods:{
            removeList:function(){
                if(confirm('本当にこのリストを削除しますか?')){
                    this.$store.dispatch('removelist',{listIndex:this.listIndex})
                }
            }
        },
        computed:{
            totalCardInList(){
                return this.cards.length
            } 
        }
    }
  
</script>