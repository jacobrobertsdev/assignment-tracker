
  
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
    position: relative;
    display: block;
    font-weight: 400;
    border-radius: 10px;
    background-color: #122034;
    padding: .5rem .9rem;
    font-size: .9rem;
  }

  h3::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -51%);
  width: 102%;
  height: 112%;
  background: linear-gradient(to top, #00acdb, #0072ff);
  z-index: -1; /* Ensure the background is behind the text */
  border-radius: 12px; /* Match the border radius of h3 */
}
  </style>