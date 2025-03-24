<script>
  import { ref, onMounted } from 'vue';
  import axios from 'axios';
  import '../assets/home.css';  

  export default {
    setup() {
      const catImage = ref('');
  
      const fetchCat = async () => {
        console.log('Button clicked');  
        try {
          const response = await axios.get('https://api.thecatapi.com/v1/images/search');  
          console.log(response.data);  
          catImage.value = response.data[0].url;  
        } catch (error) {
          console.error('Error fetching cat:', error);
        }
      };
  
      onMounted(fetchCat);  
  
      return { catImage, fetchCat };
    }
  };
</script>

<template>
  <div class="home-container">
    <h1>Here you go, random cat!</h1>
    <img v-if="catImage" :src="catImage" alt="Cat">
    <button @click="fetchCat">Gimme another</button>
  </div>
</template>
