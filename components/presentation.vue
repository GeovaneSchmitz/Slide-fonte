<template lang="pug">
  .igs-presentation-wrapper
    .igs-presentation.igs-presentation-screen(:class="`igs-breakpoint-${currentBreakpoint.index}`", ref='presentation')
      appBackground
      appSvg.igs-svg-cover(src="svg/breakpoint-cover.svg")
      appSvg.igs-svg-power-supply(src="svg/power-supply.svg")
      appSvg.igs-presentation-svg.igs-svg-fusivel(src="svg/fusivel.svg")
      appSvg.igs-presentation-svg.igs-svg-fusivel(src="svg/fusivel.svg")
      appSvg.igs-presentation-svg.igs-svg-voltimetro(src="svg/voltimetro.svg")
      appSvg.igs-presentation-svg.igs-svg-pcb1(src="svg/pcb1.svg")
      appSvg.igs-presentation-svg.igs-svg-pcb2(src="svg/pcb2.svg")
      appSvg.igs-presentation-svg.igs-svg-agradecimentos(src="svg/agradecimentos.svg")
      appSvg.igs-presentation-svg.igs-svg-problemas(src="svg/problemas.svg")
      appSvg.igs-presentation-svg.igs-svg-fonte(src="svg/fonte.svg")
      appSvg.igs-presentation-svg.igs-svg-placa(src="svg/placa.svg")
      appSvg.igs-presentation-svg.igs-svg-protoboard(src="svg/protoboard.svg")
      appSvg.igs-presentation-svg.igs-svg-ampop(src="svg/ampop.svg")
      appCircuit(ref='circuit5v' wiresSrc="svg/5v_wire.svg", componentsSrc="svg/5v.svg")
      appCircuit(ref='circuitRetificacao' wiresSrc="svg/reticacao_wire.svg", componentsSrc="svg/reticacao.svg")
      appCircuit(ref='circuitTensao' wiresSrc="svg/tensao_wire.svg", componentsSrc="svg/tensao.svg")
      appCircuit(ref='circuitCorrente' wiresSrc="svg/corrente_wire.svg", componentsSrc="svg/corrente.svg")
      appCircuit(ref='circuitPic' wiresSrc="svg/pic_wire.svg", componentsSrc="svg/pic.svg")
      appCircuit(ref='circuitDisplays' wiresSrc="svg/displays_wire.svg", componentsSrc="svg/displays.svg")
      appCircuit(ref='circuitTransformador' wiresSrc="svg/transformador_wire.svg", componentsSrc="svg/transformador.svg")
      appSvg.igs-presentation-svg.igs-svg-transformador(src="svg/transformador.svg")
      appSvg.igs-presentation-svg.igs-svg-title(src="svg/title.svg")
      appBreakpointLabel(:currentBreakpoint="currentBreakpoint")
</template>

<script>
import appBackground from '@/components/background.vue'
import appCircuit from '@/components/circuit.vue'
import appBreakpointLabel from '@/components/breakpoint-label.vue'
import appSvg from '@/components/svg.vue'
export default {
  components: {
    appBackground,
    appCircuit,
    appSvg,
    appBreakpointLabel
  },
  props: {
    currentBreakpoint: {
      type: Object,
      default () {
        return {}
      }
    },
    print: {
      type: Boolean,
      default: false
    },
    printBreakpoints: {
      type: Array,
      default () {
        return []
      }
    }
  },
  data () {
    return {
    }
  },
  mounted () {
    this.$root.$on('breakpoint-change', (breakpoint) => {
      if (this.$refs[this.currentBreakpoint.index]) {
        this.$refs[this.currentBreakpoint.index].setDisable()
      }
      if (this.$refs[breakpoint.index]) {
        this.$refs[breakpoint.index].setEnable()
      }
      if (breakpoint.index === 'cover') {
        this.powerSupplyAnimationInteval = this.powerSupplyAnimation()
      } else {
        clearInterval(this.powerSupplyAnimationInteval)
      }
    })
  },
  methods: {
    powerSupplyAnimation () {
      const currentTextElement = document.querySelector('tspan[data-powersupply="current"]')
      const currentTextShadowElement = document.querySelector('tspan[data-powersupply="current-shadow"]')
      const voltageTextElement = document.querySelector('tspan[data-powersupply="voltage"]')
      const voltageTextShadowElement = document.querySelector('tspan[data-powersupply="voltage-shadow"]')
      return setInterval(() => {
        const current = Math.trunc((0.9 + 0.1 * Math.random()) * 100) / 100
        const voltage = Math.trunc((14.9 + 0.1 * Math.random()) * 100) / 100
        currentTextElement.innerHTML = current
        currentTextShadowElement.innerHTML = current
        voltageTextElement.innerHTML = voltage
        voltageTextShadowElement.innerHTML = voltage
      }, 600)
    }
  }
}
</script>

<style>
.igs-presentation-svg > svg{
  transform: translate(5em, 0);
  width:100% !important;
  transition: all .5s;
  height: 100% !important;
  z-index: 1;
  position: absolute;
  opacity:0;
}

.igs-breakpoint-fusivel > .igs-svg-fusivel > svg,
.igs-breakpoint-ampop > .igs-svg-ampop > svg,
.igs-breakpoint-pcb2 > .igs-svg-pcb2 > svg,
.igs-breakpoint-pcb1 > .igs-svg-pcb1 > svg,
.igs-breakpoint-problemas > .igs-svg-problemas > svg,
.igs-breakpoint-agradecimentos > .igs-svg-agradecimentos > svg,
.igs-breakpoint-voltimetro > .igs-svg-voltimetro > svg,
.igs-breakpoint-protoboard > .igs-svg-protoboard > svg,
.igs-breakpoint-fonte > .igs-svg-fonte > svg,
.igs-breakpoint-placa > .igs-svg-placa > svg,
.igs-breakpoint-cover > .igs-svg-power-supply > svg{
  width:100%;
  transform: translate(0, 0);
  position: absolute;
  opacity: 1;
  height: 100%;
  background-size: contain;
}
.igs-breakpoint-cover > .igs-svg-cover > svg{
  width:100% !important;
  transform: translate(0, 0);
  position: absolute;
  opacity: 1;
  height: 100% !important;
  background-size: contain;
}

.igs-breakpoint-first > .igs-svg-power-supply > svg{
  transition: all .5s;
  position: absolute;
  opacity:0;
}
.igs-breakpoint-first > .igs-svg-cover > svg{
  opacity:0;
  position: absolute;
  z-index: 1;
}

.igs-svg-power-supply > svg{
  transform: translate(62.78517870885em, -16.8232379315em);
  width:100% !important;
  height: 100% !important;
  transition: all 1s;
  z-index: 1;
  position: absolute;
  opacity:0;

}
.igs-svg-cover > svg{
  transform: translate(5em, 0);
  width:100% !important;
  transition: all .5s;
  height: 100% !important;
  z-index: 1;
  position: absolute;
  opacity:0;
}

.igs-svg-cover > svg{
  transform: translate(5em, 0);
  width:100% !important;
  transition: all .5s;
  height: 100% !important;
  z-index: 1;
  position: absolute;
  opacity:0;
}

.igs-breakpoint-first > .igs-svg.igs-svg-title > svg,
.igs-breakpoint-cover > .igs-svg.igs-svg-title > svg{
  transform: translate(5em, 0);
  opacity:0;
}
.igs-presentation-svg.igs-svg-title > svg{
  transform: translate(0, 0);
  opacity:1;
}
.igs-presentation {
  z-index: 0;
  user-select: none;
  overflow: hidden;
  display:none;
}

@media screen {
  .igs-presentation-screen{
    display: block;
  }
  .igs-presentation-wrapper {
    overflow: hidden;
    background-color: #000;
    width: 100vw;
    height: 100vh;
    position: absolute;
    display: flex;
    justify-items: center;
    align-content: center;
    align-items: center;
    z-index: 0;
  }
  .igs-presentation {
    height: 56.25vw;
    width: 100vw;
    font-size: 1vw;
    position: absolute;
  }
}
@media screen and (min-aspect-ratio: 16/9) {
  .igs-presentation-wrapper {
    flex-direction: column;
  }
  .igs-presentation {
    height:100vh;
    width: 177.77777777vh;
    font-size: 1.7777777777vh;
  }
}
@media print {
  .igs-presentation {
    width: 1920px !important;
    height: 1080px !important;
    font-size: 19.2px !important;
  }
  .igs-presentation-print{
    display: block;
  }
}
</style>
