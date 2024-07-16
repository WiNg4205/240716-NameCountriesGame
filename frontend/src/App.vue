<script setup>
  import { ref } from 'vue'
  import countries from './countries'

  let remaining_countries = ref(countries)
  let userInput = ref('')
  let named_countries = ref([])

  const enter = () => {
    const removeIndex = remaining_countries.value.indexOf(userInput.value)
    
    if (removeIndex !== -1) {
      const new_country = remaining_countries.value.splice(removeIndex, 1)
      named_countries.value.unshift(new_country)
    }

    userInput.value = ''
  }
</script>

<template>
  <header>
    <h2>Name as many countries as you can!</h2>
  </header>

  <main>
    <input v-model="userInput" @keyup.enter="enter">
    <button @click="enter">Enter</button>
    <p>Countries remaining: {{ remaining_countries.length }}</p>
    <div class="overflow">
      <span v-if="named_countries.length === 0">No countries yet!</span>
      <li v-else v-for="country in named_countries" :key="country">
        {{ country[0] }}
      </li>      
    </div>
  </main>
</template>

<style scoped>
  .overflow {
    overflow-y: auto;
    max-height: calc(100vh - 12em);
    border: 1px solid #ccc;
    padding: 1em;
    width: 16em;
  }
</style>
