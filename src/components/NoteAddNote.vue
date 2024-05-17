<template>
    <form action="" @submit.prevent="submitSurvey">
        <label for="">Title : </label>
        <input type="text" v-model="title">
        <br><br>
        <label for="">Content : </label>
        <textarea v-model="content"> </textarea>
        
        <br><br>
        

        <input type="submit" value="submit" @click="sendAddNote">
    </form>
</template>
<script>
export default{
    data(){
        return{
            title:'',
            content:''
        }
    },
    methods:{
        sendAddNote(){
            if(this.title.trim() == '' || this.content.trim() ==''){               
                return;
            }
            fetch('https://vue-test-92430-default-rtdb.firebaseio.com/surveys.json',{
                method: 'POST',
                headers:{
                    'Content-Type':'application/json'                   
                },
                body:JSON.stringify({
                    title:this.title,
                    content:this.content
                })
            });
            this.title ='';
            this.content ='';
            $emit('close-window',isShowAddNode=false)
            
        }
    }
}
</script>
<style>
input, textarea{
    width: 100%;
    border-radius: 8px;
    border: 1px solid black;
}
textarea{
    height: 10rem;
}
</style>