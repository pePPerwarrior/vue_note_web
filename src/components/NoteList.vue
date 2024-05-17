<template>
    <div >
        <div class="addNoteBlock" v-if="isShowAddNode">
            <NoteAddNote></NoteAddNote>
        </div>
        <ul>
            <li v-for="result in results">
                {{result.note}}
                <br>
                <span>     
                    {{ result.content }}
                </span>
                <div >
                    <button>edit</button>
                    <button>delete</button>
                </div>
                
            </li>
            <li @click="addNote();loadExperiences()" >add Note</li>
        </ul>
    </div>
</template>

<script>
import NoteAddNote  from './NoteAddNote.vue'
export default{
    components:{NoteAddNote},
    data(){
        return{
            isShowAddNode: true,
            // notes:['apple','dog','bird','tom','apple','dog','bird','tom','apple','dog','bird'],
            // content:'qwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytreweqwertyuirwertyuioiuytrewe',
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
                        note:data[id].title,
                        content:data[id].content
                    })
                    
                }
                this.results = results;
                
                
            })
            
        },
        addNote(){
            this.isShowAddNode = !this.isShowAddNode;
            
            
        },
    },
    
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
    
    border-radius: 10px;
    box-shadow:  9px 9px 18px #b3b3b3,
             -9px -9px 18px #ffffff;
    overflow-y: scroll;
}

li span {
    font-size: 12px;
    text-align: justify;
    word-wrap: break-word;
    overflow-y: scroll;
}
button {
    margin: auto;
}
.addNoteBlock{
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 400px;
    height: 300px;
    background-color: white;
    border: 1px solid #ccc;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    padding: 20px;
    border-radius: 8px;
    /* display: flex;
    flex-direction: column; */
    text-align: center;
    align-items: center;
    justify-content: center;
    z-index: 3;
}

</style>