<template>
  <div class="main-container">
    <Banner />
    <h2 class="title">Monte seu burguer</h2>
    <Form />
  </div>
</template>

<script>
import Form from '../components/Form.vue'
import Banner from '../components/Banner.vue'


export default {
  name: 'Home',
  
  components: {Banner, Form}
}
</script>


