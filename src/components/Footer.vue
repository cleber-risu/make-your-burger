<script>
  export default {
    name: 'Footer'
  }
</script>

<template>
  <footer id="footer">
    <p>Make Your Burger &copy; 2024</p>
  </footer>
</template>

<style scoped>
  #footer {
    width: 100%;
    height: 200px;
    bottom: 0;

    background-color: #222;
    border-top: 4px solid #111;

    color: #fcba03;

    display: grid;
    place-items: center;
  }
</style>