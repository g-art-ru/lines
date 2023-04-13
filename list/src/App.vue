<template>
  <div class="container">
    <LineView v-for="line in lines" :key="line.id" :msg="line" @update="Update" @delete="Delete" @hide="Hide"/>
    <LineAdd @add-lines="AddLines"></LineAdd>
  </div>
</template>

<script>
import LineView from './components/LineView.vue'
import LineAdd from './components/LineAdd.vue'
import axios from 'axios'


export default {
  name: 'App',
  components: {
    LineView,
    LineAdd
   },
   data(){
    return {
      lines: [
        {word: 'слово 1', yandex: '1', google: '2'},
        {word: 'слово 2', yandex: '2', google: '22'},
        {word: 'слово 3', yandex: '3', google: '222'}
      ]
    }
   },
   created(){
    console.log("d");
    axios.get("http://localhost:2525/words").then((response)=>{
          console.log('Done' + response.data);
          this.lines = response.data;
        })
   },
   methods:{
      removeLineWithId(id) {
        const objWithIdIndex = this.lines.findIndex((obj) => obj.id === id);

        if (objWithIdIndex > -1) {
          this.lines.splice(objWithIdIndex, 1);
        }
      },
      hideLineWithId(id){
        var fl;
        const objWithIdIndex = this.lines.findIndex((obj) => obj.id === id);
        if (objWithIdIndex > -1) {
          if(this.lines[objWithIdIndex].hide==0){fl = 1;}else{fl = 0;}
          this.lines[objWithIdIndex].hide = fl;
         
        }
        return fl;
      },
      AddLines(data){
        
        var mas = [];
        mas = data.lines.split(/\r?\n/);
        mas.forEach((el) => {
          
          let dt = {
            word: el,
            yandex: 1,
            google: 1,
            hide: 0
          }
          axios.post("http://localhost:2525/words", dt).then((response)=>{
            console.log('Done' + response.data);
          }).catch((error) => {
            console.log(error);
          });
          this.lines.push(dt);
          

        })
        
       
      },
      Update(){
        console.log("update position");
      },
      Delete(id){
        axios.delete("http://localhost:2525/words/" + id).then((response)=>{
            console.log('Done' + response.data);
        }).catch((error) => {
            console.log(error);
        });
        console.log("Delete position" + id);
        this.removeLineWithId(id);
        
      },
      Hide(id){
        
        let dt = {
          hide: this.hideLineWithId(id),
        };
        
        axios.patch("http://localhost:2525/words/" + id, dt).then((response)=>{
            console.log('Done' + response.data);
        }).catch((error) => {
            console.log(error);
        });
        
        
      }
   }
   
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
