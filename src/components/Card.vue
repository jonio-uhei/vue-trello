<template>
    <div class="card">
        <button class="close-button" @click="removeCardFromList">x</button><!--/.close-button-->
        <div class="body">{{body}}</div><!--/.body-->
    </div><!--/.card-->
</template>

<script>
    export default{
        props:{
            body:{
                type:String,
                required:true
            },
            listIndex:{
                type:Number,
                required:true
            },
            cardIndex:{
                type:Number,
                required:true
            }
        },
        methods:{
            removeCardFromList(){
                if(confirm('本当にこのカードを削除しますか？')){
                    this.$store.dispatch('removeCardFromList',{cardIndex:this.cardIndex,listIndex:this.listIndex})
                }
            }
        }
    }
</script>               