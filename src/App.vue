<script>
  import Navbar from '@/components/Navbar.vue'
  import Footer from '@/components/Footer.vue'

  export default {
    data() {
      return {
        logSrc: '/img/logo.png',
        appName: 'Make Your Burger'
      }
    },
    components: {
      Navbar,
      Footer
    }
  }
</script>
<template>
  <div>
    <Navbar :logo="logSrc" :alt="appName" />
    <router-view/>
    <Footer />
  </div>
</template>

<style>
  * {
    font-family: Helvetica, sans-serif;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .main-container {
    margin: 50px;
    min-height: calc(100vh - 380px);
  }

  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }
</style>
