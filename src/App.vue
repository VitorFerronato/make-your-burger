<template>
  <NavbarApp :logo='logo_src' :alt='app_name'/>
  <router-view/>
</template>

<script>
import NavbarApp from './components/NavbarApp.vue'

export default {
  components: { NavbarApp},

  data() {
    return{
      logo_src: '/img/logo.png',
      app_name: 'Make your burger'
    }
  }
  
}
</script>

<style>
  /* =============== Global Vars =============== */
  :root{
    --font-family: Helvetica;

    --first-color: #fcba03;
    --dark-color:  #222;
  }

  /* =============== Global Classes =============== */
  h2{
    text-align: center;
    font-size: 42px;
    margin: 1rem 0;
    color: var(--dark-color);
  }

  /* =============== Reset Styles =============== */
  *{
    font-family: var(--font-family);
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
</style>
