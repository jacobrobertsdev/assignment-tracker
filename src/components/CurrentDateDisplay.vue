  <script setup>
  import { ref, onMounted } from 'vue'
  
  const formattedDateTime = ref('')
  
  onMounted(() => {
    const now = new Date()
  
    const options = { 
      hour: 'numeric', 
      minute: '2-digit',
      month: 'numeric', 
      day: 'numeric', 
      year: 'numeric', 
    }

      formattedDateTime.value = now.toLocaleDateString(undefined, options).replace(',', ' - ')
    
  })
  </script>

  <template>
      <h3>{{ formattedDateTime }}</h3>
  </template>

  <style scoped>

  h3 {
    margin: 0 auto;
    position: relative;
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
    background: linear-gradient(to top, #0097c1, #1c7ed6);
    z-index: -1;
    border-radius: 12px; 
}
  </style>