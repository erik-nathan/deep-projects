<template>
  <div class="home">
  <CategoryMenu />
  </div>
</template>

<script>
import CategoryMenu from '../components/CategoryMenu.vue'
import axios from 'axios';

export default {
  name: 'HomeView',
  components: {
    CategoryMenu
  },
  created() {
    axios.get('http://localhost:3000/products').then( response => {
      console.log(response);
    })
  }
}
</script>
