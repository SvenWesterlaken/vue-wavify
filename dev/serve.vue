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
    <vue-wavify fill="url(#gradient)">
      <defs>
        <linearGradient id="gradient">
          <stop offset="0%" style="stop-color:rgb(255,255,0);" />
          <stop offset="100%" style="stop-color:rgb(255,0,0);" />
        </linearGradient>
      </defs>
    </vue-wavify>
    <vue-wavify fill="#e62315" mask="url(#mask)" :points="20" :amplitude="25" :speed="0.2" :height="20">
      <defs>
        <mask id="mask">
          <path d="M10,35 A20,20,0,0,1,50,35 A20,20,0,0,1,90,35 Q90,65,50,95 Q10,65,10,35 Z" fill="white" />
        </mask>
      </defs>
    </vue-wavify>
    <vue-wavify mask="url(#mask2)" fill="#1277b0" >
      <defs>
        <linearGradient id="grad" gradientTransform="rotate(90)">
          <stop offset="0" style="stop-color:white;" />
          <stop offset="0.5" style="stop-color:black;" />
        </linearGradient>
        <mask id="mask2">
          <rect x="0" y="0" width="800" height="200" fill="url(#grad)"/>
        </mask>
      </defs>
    </vue-wavify>
  </div>
</template>

<style>
body {
  padding: 0;
  margin: 0;
}

#app {
  background: #f8f1f1;
}
</style>
