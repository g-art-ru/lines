<template>
  <div class="container">
    <LineView v-for="line in lines" :key="line.id" :msg="line" @update="Update" @delete="Delete" @hide="Hide"/>
    <LineAdd @add-lines="AddLines"></LineAdd>
  </div>
</template>

<script>
import LineView from './components/LineView.vue'
import LineAdd from './components/LineAdd.vue'


export default {
  name: 'App',
  components: {
    LineView,
    LineAdd
   },
   methods:{
      AddLines(data){
        console.log(data.lines);
      },
      Update(){
        console.log("update position");
      },
      Delete(){
        console.log("Delete position");
      },
      Hide(){
        console.log("Hide position");
      }
   },
   data(){
    return {
      lines: [
        {word: 'слово 1', yandex: '1', google: '2'},
        {word: 'слово 2', yandex: '2', google: '22'},
        {word: 'слово 3', yandex: '3', google: '222'}
      ]
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
