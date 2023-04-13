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
        console.log("Delete position" + id);
        axios.delete("http://localhost:2525/words/" + id).then((response)=>{
            console.log('Done' + response.data);
        }).catch((error) => {
            console.log(error);
        });
      },
      Hide(){
        console.log("Hide position");
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
