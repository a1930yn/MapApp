<template>
  <div>
    <h1>Vue.jsで地図アプリ</h1>
    <vmap></vmap>
    <vcontroller></vcontroller>
  </div>
</template>

<script>
import vmap from "./vmap"
import vcontroller from "./vcontroller"
export default{
  components:{
    vmap,
    vcontroller
  }
}
</script>

<style scoped>
div{
  width: 640px;
}
h1{
  text-align: center;
}
</style>