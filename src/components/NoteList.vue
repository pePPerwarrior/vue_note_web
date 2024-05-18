<template>
    <div >
        <!-- {{ results }} -->
        <div class="addNoteBlock" v-if="isShowAddNode">
            <NoteAddNote @closeWindow="sendAddNote"></NoteAddNote>
        </div>
        <ul>
            <li v-for="(result,key) in results" :key="key"> 
                <div style="font-size:1.5em;font-weight: bold;">
                    {{result.note}} 
                    <!--{{ key }} -->
                </div>  
                
                <!-- no.{{ key }} -->
                <span>     
                    {{ result.content }}
                </span>
                <hr>
                <div >
                    <button>edit</button>
                    <button @click="delNote()">delete</button>
                </div>
                
            </li>
            <!-- <li @click="addNote();loadExperiences()" >add Note</li> -->
            <li @click="addNote()" class="addNote" ><i class="fa-solid fa-plus"></i></li>
        </ul>
    </div>
</template>

<script>
import NoteAddNote  from './NoteAddNote.vue'
export default{
    components:{NoteAddNote},
    data(){
        return{
            isShowAddNode: false,
            results:[],
        }
    },
    methods:{
        loadExperiences() {
            // this.results = [];
            fetch('https://vue-test-92430-default-rtdb.firebaseio.com/surveys.json')
            .then((response) => {
                if (response.ok) {
                    return response.json();
                }
            })
            .then((data) => {
                const results = [];
                for (const id in data) {
                    results.push({
                        id:id,
                        note:data[id].title,
                        content:data[id].content
                    })               
                }
                this.results = results;
                console.log(this.results);
            })
            
        },
        // sendAddNote(val1,val2){
        //     this.isShowAddNode = false;
        //     if(val1 > 1){                   
        //     // 當一個欄位不為空時 推送進results印出 (暫存區)    
        //     this.results.push({
        //                 id:0,
        //                 note:val1,
        //                 content:val2
        //             }) 
        //     console.log(this.results); 
        //     }
        // },
        sendAddNote(){
            this.isShowAddNode = false;
            setTimeout(this.loadExperiences,1000); //延遲載入
        },
        addNote(){
            this.isShowAddNode = !this.isShowAddNode; 
              
        },
        delNote(){

        }
        
    },
    mounted(){
        this.loadExperiences();
    }
    
}
</script>
<style scoped>
ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
    display: flex;
    flex-wrap: wrap;
    text-align: center;
    justify-content: space-evenly
}

li {
    background-color: #fff385;
    margin: 5px 0;
    padding: 20px;
    border-radius: 8px; /* Rounded corners */
    position: relative;
    align-items: center;
    justify-content: space-between; /* Added to align buttons to the right */
    height: 200px;
    width: 200px;
    margin: 10px;
    word-wrap: break-word;
    display:block;
    border-radius: 10px;
    box-shadow:  9px 9px 18px #b3b3b3,
             -9px -9px 18px #ffffff;
    overflow-y: scroll;
    scrollbar-width: 100px;
}
.addNote{
    background-color: #f9f9f9;
    border: 1px solid #ddd;
    padding: 20px;
    border-radius: 8px;
    height: 200px;
    width: 200px;
    margin: 10px;
    cursor: pointer;
    display: flex;
    justify-content: center;
    align-items: center;
}
li i {
    font-size: 70px;
    color: gainsboro;
}

li span {
    display: block;
    font-size: 1em;
    text-align: justify;
    word-wrap: break-word;
    overflow-y: scroll;
    padding: 1rem 0;
    
}
button {
    margin: auto;
}
::-webkit-scrollbar {
    width: 0px;
    background: transparent; /* make scrollbar transparent */
}


</style>