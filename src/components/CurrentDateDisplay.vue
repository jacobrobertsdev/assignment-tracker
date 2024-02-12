
  
  <script setup>
  import { ref, onMounted } from 'vue';
  
  const formattedDateTime = ref('');
  
  onMounted(() => {
    const now = new Date();
  
    const options = { 
      hour: 'numeric', 
      minute: '2-digit',
      month: 'numeric', 
      day: 'numeric', 
      year: 'numeric', 
      
    };
  
    formattedDateTime.value = now.toLocaleDateString(undefined, options).replace(',',' - ')
  });
  </script>
  <template>
   
      <h3>{{ formattedDateTime }}</h3>

  </template>
  <style scoped>
  h3 {
    font-weight: 400;
    border-radius: 10px;
    background-color: #122034;
    padding: 1rem;
    margin:1rem auto;
    font-size: .9rem;
  }
  </style>