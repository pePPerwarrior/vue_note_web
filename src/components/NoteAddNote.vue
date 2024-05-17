<template>
    <form action="" @submit.prevent="submitSurvey">
        <label for="">Title : </label>
        <input type="text" v-model="title" class="title">
        <br><br>
        <label for="">Content : </label>
        <textarea v-model="content"> </textarea>
        
        <br><br>
        

        <input type="submit" value="submit" @click="sendAddNote" class="bottomBtn">
        <button  @click="close" class="bottomBtn">close</button>
    </form>
</template>
<script>
export default{
    emits:['close-window'],
    data(){
        return{
            title:'',
            content:''
        }
    },
    methods:{
        close(){
            this.$emit('close-window')
        },
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
            // this.$emit('close-window',this.title.trim(),this.title.trim());
            this.$emit('close-window');
            this.title ='';
            this.content ='';
            
        }
    }
}
</script>
<style>
form{
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 30vw;
    max-width: 400px;
    height: 300px;
    background-color: white;
    border: 1px solid #ccc;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    padding: 20px;
    border-radius: 8px; 
    text-align: center;
    align-items: center;
    justify-content: center;
    z-index: 3;
}
.title{
    height: 2rem;
    width: 100%;
    border-radius: 4px;
    border: 1px solid black;
    font-size: 1.2rem;
}
textarea{
    width: 100%;
    height: 10rem;
    font-size: 1.2rem;
    border-radius: 4px;
    border: 1px solid black;
}
.bottomBtn{
    width: 30%;
    margin: 0px 20px ;
    border-radius: 8px;
    font-size: 1.2rem;
    border: 1px solid black;
}
</style>