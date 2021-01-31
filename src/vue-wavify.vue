<template>
<div class="vue-wavify-wave" ref="wave" v-on="$listeners">
  <svg version="1.1" xmlns="http://www.w3.org/2000/svg" v-bind="$attrs">
    <slot></slot>
    <path :d="this.path" :fill="fill"/>
  </svg>
</div>
</template>

<script>
export default {
  name: 'VueWavify',
  inheritAttrs: false,
  props: {
    paused: {
      default: false,
      type: Boolean
    },
    points: {
      default: 3,
      type: Number
    },
    speed: {
      default: 0.15,
      type: Number
    },
    height: {
      default: 20,
      type: Number
    },
    amplitude: {
      default: 20,
      type: Number
    },
    fill: {
      default: 'blue',
      type: String
    }
  },
  data() {
    return {
      path: '',
      lastUpdate: 0,
      elapsed: 0,
      step: 0
    }
  },
  mounted() {
    if (!this.$frameId) {
      this.resume();
    }
  },
  beforeDestroy() {
    window.cancelAnimationFrame(this.$frameId);
    this.$frameId = 0;
  },
  methods: {
    containerWidth () {
      return this.$refs.wave.offsetWidth;
    },
    containerHeight () {
      return this.$refs.wave.offsetHeight;
    },
    calculateWavePoints () {
      const points = [];
      for (let i = 0; i <= Math.max(this.points, 1); i ++) {
        const scale = 100;
        const x = i / this.points * this.containerWidth();
        const seed = (this.step + (i + i % this.points)) * this.speed * scale;
        const height = Math.sin(seed / scale) * this.amplitude;
        const y = Math.sin(seed / scale) * height  + this.height;
        
        points.push({x, y});
      }
      return points;
    },
    buildPath (points) {
      let svg = `M ${points[0].x} ${points[0].y}`;

      const initial = {
        x: (points[1].x - points[0].x) / 2,
        y: (points[1].y - points[0].y) + points[0].y + (points[1].y - points[0].y)
      };

      const cubic = (a, b) => ` C ${a.x} ${a.y} ${a.x} ${a.y} ${b.x} ${b.y}`;
      svg += cubic(initial, points[1]);

      let point = initial;

      for (let i = 1; i < points.length - 1; i ++) {
        point = {
          x: (points[i].x - point.x) + points[i].x,
          y: (points[i].y - point.y) + points[i].y
        };
        svg += cubic(point, points[i + 1]);
      }

      svg += ` L ${this.containerWidth()} ${this.containerHeight()}`;
      svg += ` L 0 ${this.containerHeight()} Z`;

      return svg;
    },
    redraw () {
      this.path = this.buildPath(this.calculateWavePoints());
    },
    draw () {
      if (!this.paused) {
        const now = new Date();
        
        this.elapsed += (now - this.lastUpdate);
        this.lastUpdate = now;
      }
      const scale = 1000;

      this.step = this.elapsed * Math.PI / scale;
      this.redraw();
    },
    update () {
      this.draw();
      if (this.$frameId) {
        this.resume();
      };
    },
    resume () {
      this.$frameId = window.requestAnimationFrame(this.update);
      this.lastUpdate = new Date();
    }
  }
};
</script>


<style scoped>
.vue-wavify-wave {
  display: inline-block;
  width: 100%;   
}

.vue-wavify-wave svg {
  width: 100%;
  height: 100%;
}
</style>
