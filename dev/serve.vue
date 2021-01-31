<script>
import Vue from 'vue';
import VueWavify from '@/vue-wavify.vue';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    VueWavify
  }
});
</script>

<template>
  <div id="app">
    <vue-wavify />
  </div>
</template>
