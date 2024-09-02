<template>
  <navBar :logo="logo_src" :alt="app_name" />
  <router-view/>
  <fooTer/>
</template>

<script>
import navBar from './components/Navbar.vue'
import fooTer from './components/Footer.vue'

export default {
  components:{
    navBar,
    fooTer
  },
  data(){
    return{
      logo_src: "/img/logo.png",
      app_name: "Make Your Potion"
    }
  }
}
</script>

<style>
  * {
    font-family: Helvetica;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .main_container {
    margin: 50px;
    min-height: 500px;
  }

  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }

</style>