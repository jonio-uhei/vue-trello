<template>
    <form :class="classList" @submit.prevent="addList">
        <input 
            v-model="title"
            type="text"
            class="text-input"
            placeholder="リストを追加"
            @focusin="startEditing"
            @focusout="finishEditing"
        >
        <button 
            type="submit" 
            class="add-button"
            v-if="isEditing || titleExists"
        >Add</button>
    </form>
</template>

<script>
export default{
    data:function(){
        return {
            title:'',
            isEditing:false
        }
    },
    computed:{
        titleExists(){
            return this.title.length > 0
        },
        classList(){
            const classList = ['addlist']
            if(this.isEditing){
                classList.push('active')
            }
            if(this.titleExists){
                classList.push('addable')
            }
            return classList
        }
    },
    methods:{
        addList:function(){
            this.$store.dispatch('addlist',{title:this.title})
            this.title = ''
        },
        startEditing(){
            this.isEditing = true
        },
        finishEditing(){
            this.isEditing = false
        }
    }
}
</script>