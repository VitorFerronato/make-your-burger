<template>
    <div id="main-banner">
        <h1>Make your burguer</h1>
    </div>
</template>

<script>
export default {
    name: 'Banner'
}
</script>

<style scoped>
  #main-banner{
    background-image: url('/public/img/burger.jpg');
    background-position: 0 -250px;
    background-size: cover;
    background-repeat: no-repeat;
    height: 75vh;
    display: flex;
    align-items: center;
    justify-content: flex-start;
  }

  #main-banner h1 {
    color: #FFF;
    text-align: center;
    font-size: 60px;
    background-color: var(--dark-color);
    padding: 20px 40px;
    margin-left: 1rem;
  }
</style>

