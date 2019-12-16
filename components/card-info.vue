<template lang="pug">
  .igs-card-info
      .igs-card-info-content
        .igs-card-header
          .igs-card-info-title
            |Informações
          .igs-card-close-button(@click='close')
        .igs-card-info-text
          |Esta apresentação foi feita com nuxt.js, caso você sinta interesse em desenvolver uma apresentação similar ou entender como foi feita as animações, você pode acessar todo o código fonte
          a.igs-card-link(href='https://github.com/GeovaneSchmitz/Slide-fonte', rel="noopener noreferrer")  aqui
          |, e caso sinta alguma dúvida fale comigo.
          a.igs-card-link.igs-card-contacts(href='https://www.geovanems.com.br/pt/contacts', rel="noopener noreferrer")  Meus contatos
        .igs-card-info-signature
          |Geovane Schmitz em 14 de Dezembro de 2019
</template>

<script>
export default {
  props: {
  },
  data () {
    return {}
  },
  mounted () {},
  methods: {
    close () {
      this.$root.$emit('card-close')
    }
  }
}
</script>

<style>
.igs-card-info {
  position: absolute;
  width: 100vw;
  z-index: 3;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(0,0,0,.2)
}
.igs-card-close-button{
  background-image: url(../assets/close-button.svg);
  width: 2rem;
  height: 2rem;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
}
.igs-card-contacts{
  display:block;
  font-size:1.1em;
  text-indent: 0;
  margin-top: 0.2em;
}
.igs-card-header{
  padding: 0 0em 0.5em 0em;
  margin-bottom: 1em;
  display: flex;
  justify-content: space-between;
  border-bottom: 2px  solid #0035ca;
}
.igs-card-link{
  text-decoration: none;
  color:#0035ca !important;
}
.igs-card-info-title {
  color: #0035ca;
  font-family: 'Josefin Sans';
  font-size:1.5rem;
}
.igs-card-info-text {
  text-indent: 1em;
  line-height: 1.5;
}
.igs-card-info-signature {
  color: #0035ca;
  font-size:1.1em;
  margin-top: 1em;
}
.igs-card-info-content {
  max-width: 960px;
  box-shadow: 0 0.5rem 1rem 0rem rgba(47, 64, 176, 0.1);
  padding: 2em;
  font-size:1rem;
  margin:1rem;
  color: rgba(0,0,0,0.8);
  border-radius: 5px;
  background-color: #fff;
  font-family: 'Josefin Sans'
}
</style>
