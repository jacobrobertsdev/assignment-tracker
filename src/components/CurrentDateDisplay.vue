<script setup>
  import { ref, onMounted, onBeforeUnmount } from 'vue'

  const formattedDateTime = ref('')
  let intervalId // Declare intervalId outside of the setup to keep track of the interval

  const setDateTime = () => {
    const current = new Date()
    const options = {
      hour: 'numeric',
      minute: '2-digit',
      month: 'numeric',
      day: 'numeric',
      year: 'numeric',
    }

    formattedDateTime.value = current.toLocaleDateString(undefined, options).replace(',', ' - ')
  }

  const scheduleUpdate = () => {
    const current = new Date()
    const seconds = 60 - current.getSeconds() // Calculate seconds left in the current minute

    clearInterval(intervalId)// Clear previous interval
    intervalId = setInterval(setDateTime, seconds * 1000) // Update time on calculated interval
  }

  onMounted(() => {
    setDateTime() // Initial call to set the date time
    scheduleUpdate() // Schedule the next update
  })

  // When the component is unmounted, clear the interval
  onBeforeUnmount(() => {
    clearInterval(intervalId)
  })
</script>

  <template>
      <h3>{{ formattedDateTime }}</h3>
  </template>

  <style scoped>

  h3 {
    margin: 1rem auto;
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
    transform: translate(-50%, -50%);
    width: 102%;
    height: 112%;
    background: linear-gradient(to top, #0097c1, #1c7ed6);
    z-index: -1;
    border-radius: 12px; 
}
  </style>