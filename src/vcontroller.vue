<template>
  <div>
    <div id="mycontroller">
      <div id="mypad">
        <v-fa class="pad" icon="long-arrow-alt-left" />
        <v-fa class="pad" icon="long-arrow-alt-up" />
        <v-fa class="pad" icon="long-arrow-alt-right" />
        <v-fa class="pad" icon="long-arrow-alt-down" />
      </div>
    </div>
  </div>
</template>

<script>

// Fontawesome
import Vue from "vue";
import { library } from '@fortawesome/fontawesome-svg-core';
import { fas } from '@fortawesome/free-solid-svg-icons';
import { far } from '@fortawesome/free-regular-svg-icons';
import { fab } from '@fortawesome/free-brands-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
library.add(fas, far, fab);
Vue.component('v-fa', FontAwesomeIcon);

export default{
  name: "vcontroller"
}
</script>

<style scoped>
#mycontroller{
  width: 480px;
  margin-top: 20px;
  margin-left: auto;
  margin-right: auto;
}
#mypad{
  display: flex;
  justify-content: space-around;
}
.pad{
  display: block;
  width: 30px;
  height: 30px;
  border: 1px solid black;
}
</style>