<template>
  <div>
    <!--h1>Application system using the common EWS message </h1-->
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
  width: 900px;
}
h1{
  text-align: center;
}
</style>