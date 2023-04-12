<template>
  <div class="row mb-3">
    <div class="col-lg-4 col-md-4 col-sm-6 col-6">
      <textarea name="" id="" cols="30" rows="10" class="form-control mb-3" v-model="lines"></textarea>
      <button class="btn btn-primary" @click="sendLines">Добавить</button>
    </div>
    <div class="col-lg-1 col-md-1 col-sm-3 col-3">
     
    </div>
    <div class="col-lg-1 col-md-1 col-sm-3 col-3">
      
    </div>
    <div class="col-lg-3 col-md-3 col-sm-3 col-3">
      
    </div>
  </div>
</template>

<script>
export default {
  name: 'LineAdd',
  data(){
    return{
      lines: ''
    }
  },
  methods:{
    sendLines(){
      this.$emit('addLines', { lines: this.lines });
      this.lines = '';
    }
  },
  emits: ['addLines'],
  props: {
    msg: Object
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
