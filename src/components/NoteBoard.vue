<template>
    <div class="board">
        <!-- <NoteHeader></NoteHeader> -->
        
        <NoteList></NoteList>
    </div>
    
</template>

<script>
import NoteList from './NoteList.vue';
import NoteHeader from './NoteHeader.vue';
export default{
    components:{
        NoteList,
        NoteHeader
    }
}
</script>

<style scoped>
.board{
    
    background-color: #fff;
    border-radius: 8px;
    box-shadow: 0px 10px 15px 10px rgba(0, 0, 0, 0.3);
    overflow: hidden;
    width: 60vw;
    height: 600px;
    padding: 20px;
    box-sizing: border-box;
    text-align: center;
    align-items: center;
    justify-content: center;
    overflow-y: scroll;
    position: relative;
}



</style>