<template lang='pug'>
  .igs-index
    transition(name='igs-card-fade')
      appCardInfo(v-if="showCard")
    toolbar(:currentBreakpoint="currentBreakpoint")
    presentation.igs-index-presentation(:currentBreakpoint="currentBreakpoint")
</template>

<script>
import toolbar from '@/components/toolbar.vue'
import presentation from '@/components/presentation.vue'
import breakpoints from '@/breakpoints'
import appCardInfo from '@/components/card-info.vue'

export default {
  components: {
    toolbar,
    appCardInfo,
    presentation
  },
  data () {
    return {
      breakpoints,
      breakpointIndex: 0,
      showCard: true,
      currentBreakpoint: breakpoints[0]
    }
  },
  created () {
    this.printBreakpoints = breakpoints.filter((breakpoint) => {
      return !breakpoint.noPrint
    })
  },
  mounted () {
    this.$root.$on('card-close', this.startPresentation)
  },
  methods: {
    startPresentation () {
      this.showCard = false
      this.$root.$on('request-to-previous', this.toPrevious)
      this.$root.$on('request-to-next', this.toNext)
      window.addEventListener('keyup', this.keyboardEvent)
    },
    keyboardEvent (event) {
      const keysNextBreakpoint = ['ArrowRight', ' ', 'Enter']
      const keysPreviousBreakpoint = ['ArrowLeft']
      if (keysNextBreakpoint.includes(event.key)) {
        this.toNext()
      } else if (keysPreviousBreakpoint.includes(event.key)) {
        this.toPrevious()
      }
    },
    toNext () {
      if (!(this.breakpointIndex + 1 === this.breakpoints.length)) {
        this.breakpointIndex++
        this.currentBreakpoint = this.breakpoints[this.breakpointIndex]
        this.$root.$emit('breakpoint-change', this.currentBreakpoint)
        if (this.currentBreakpoint.autoplay) {
          setTimeout(this.toNext, this.currentBreakpoint.timeout)
        }
      }
    },
    toPrevious () {
      if (this.breakpointIndex > 0) {
        this.breakpointIndex--
        this.currentBreakpoint = this.breakpoints[this.breakpointIndex]
        this.$root.$emit('breakpoint-change', this.currentBreakpoint)
        if (this.currentBreakpoint.autoplay) {
          setTimeout(this.toPrevious, this.currentBreakpoint.timeout)
        }
      }
    }
  }
}
</script>

<style>
.igs-card-fade-enter-active, .igs-card-fade-leave-active{
  transition: all .25s;
}
.igs-card-fade-enter, .igs-card-fade-leave-to{
  opacity: 0;
  transform: translateY(20px)
}
.igs-card-fade-enter-to, .igs-card-fade-leave{
  opacity: 1;
  background-color: #f00;
}
.igs-index{
  background-color: #000;
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
}
</style>
