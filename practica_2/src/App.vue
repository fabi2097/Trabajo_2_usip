<template>
  <div>
  <Menu></Menu>    
  <router-view/> 
  </div>
  <Footer></Footer>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

</style>
<script>
import Menu from '@/components/Menu.vue';
import Footer from '@/components/Footer.vue';
export default {
  name: 'App',
  data(){
    return {
    }
  },
  methods: {
    
  },
  components:{
    Menu,Footer
  }
}
</script>