<script>
  import { ref, onMounted } from 'vue';
  import axios from 'axios';
  import '../assets/info.css';  

  export default {
    setup() {
      const catImage = ref('');
      const catFact = ref('');
      const catFacts = ref([
        "Cats are known for their independence.",
        "Cats sleep for about 70% of their lives.",
        "A group of cats is called a clowder.",
        "Cats can make over 100 different sounds.",
        "The average cat sleeps for 13-16 hours a day.",
        "Cats are mammals",
        "Everyone should have a cat",
        "Im running out of facts",
        "If you want more, go check google",
        "This one is funny isn't it"
      ]);
  
      
      const fetchCatInfo = async () => {
        try {
          const response = await axios.get('https://api.thecatapi.com/v1/images/search');  
          catImage.value = response.data[0].url;  
          
          
          const randomFactIndex = Math.floor(Math.random() * catFacts.value.length);
          catFact.value = catFacts.value[randomFactIndex];  
        } catch (error) {
          console.error('Error fetching cat info:', error);
        }
      };
  
      onMounted(fetchCatInfo);  
  
      return { catImage, catFact, fetchCatInfo };
    }
  };
</script>

<template>
  <div class="info-container">
    <h1>You wanna know more huh!</h1>
    <div v-if="catImage">
      <img :src="catImage" alt="Cat" />
    </div>
    <div v-if="catFact">
      <p><strong>Fun Fact:</strong> {{ catFact }}</p>
    </div>
    <button @click="fetchCatInfo">And another one!</button>
  </div>
</template>
