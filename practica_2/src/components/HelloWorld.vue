<template>
  <div>
    <H1>MegaDron</H1>
    <H2>Diplomado modulo 6</H2>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props:{
    idhijo:null
  },
  data(){
    return {}; //devolver un objeto vacío
  },
  methods:{
    emitirmensaje(id){
      this.idhijo=id;
      alert("el componente hijo recibio"+this.idhijo);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

</style>
