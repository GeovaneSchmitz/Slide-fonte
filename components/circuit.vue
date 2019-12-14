<template lang="pug">
  .igs-circuit
    appSvg.igs-circuit-svg.igs-circuit-wire(:src='wiresSrc')
    appSvg.igs-circuit-svg.igs-circuit-components(:src='componentsSrc')
</template>

<script>

import appSvg from '@/components/svg.vue'

export default {
  components: {
    appSvg
  },
  props: {
    wiresSrc: {
      type: String,
      required: true
    },
    componentsSrc: {
      type: String,
      required: true
    }
  },
  data () {
    return {}
  },
  mounted () {
  },
  methods: {
    setEnable () {
      this.$el.classList.add('igs-circuit-active')
    },
    setDisable () {
      this.$el.classList.remove('igs-circuit-active')
    }
  }
}
</script>

<style>
.igs-circuit-active .igs-circuit-wire svg path {
  stroke-dasharray: 6000;
  stroke-dashoffset: 6000;
  animation: dash 4s ease-in-out;
  animation-fill-mode: forwards;
}

@keyframes dash {
  to {
    stroke-dashoffset: 0;
  }
}

.igs-circuit-svg svg{
  position: absolute;
  width: 92em;
  height: 42.25em;
  opacity: 0;
  transform: translate(5em, 0);
  transition: all .5s;
}

.igs-circuit-wire svg{
  position: absolute;
  width: 92em;
  height: 42.25em;
  opacity: 0;
  transition: all 0.5s;
}
.igs-circuit-active svg {
  opacity: 1;
  transform: translate(0, 0)
}
.igs-circuit{
  width: 92em;
  margin: 10em 4em 4em 4em;
  height: 42.25em;
  overflow: hidden;
  position: absolute;
}
</style>
