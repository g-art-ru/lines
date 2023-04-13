<template>
  <div class="row mb-3">
    <div class="col-lg-4 col-md-4 col-sm-6 col-6">
      <input type="text" class="form-control" id="word-1" :value="msg.word">
    </div>
    <div class="col-lg-1 col-md-1 col-sm-3 col-3">
      <input type="number" class="form-control" id="yandex-1" disabled :value="msg.yandex">
    </div>
    <div class="col-lg-1 col-md-1 col-sm-3 col-3">
      <input type="number" class="form-control" id="google-1" disabled :value="msg.google">
    </div>
    <div class="col-lg-3 col-md-3 col-sm-3 col-3">
      <div class="button-group" role="group">
        <button type="button" class="btn btn-primary" @click="$emit('update')" alt="Обновить"><i class="bi bi-arrow-clockwise"></i></button>
        <button type="button" class="btn btn-warning" @click="$emit('hide')"  alt="Скрыть"><i class="bi bi-eye-slash"></i></button>
        <button type="button" class="btn btn-danger" @click="$emit('delete', msg.id)" alt="Удалить"><i class="bi bi-trash3"></i></button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LineView',
  props: {
    msg: Object
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
