<script setup lang="ts">
  import { ref, inject } from 'vue'

  const axios: any = inject('axios')

  const selectedCity = ref('');

  const emit = defineEmits<{
    (event: 'selectedCity', city: string): void
  }>();

  const submitCity = () => {
    console.log("selectedCity in child : ", selectedCity)
    emit('selectedCity', selectedCity.value)
    selectedCity.value = ''
  }
</script>

<template>
    <div>
        <input v-model="selectedCity" type="search" placeholder="Nom de ville / village" name="rechercheVille" id="rechercheVille" ref="rechercheVille" @keyup.enter="submitCity">
        <button @click="submitCity"/>
    </div>
</template>

<style scoped>
    div {
        display: flex;
        margin: auto;
        width: 240px;
        max-width: 240px;
        padding: 2px;
        border: 1px solid;
        border-radius: 5px;
    }

    input[type="search"] {
     padding: 15px;
     border-radius: 5px;
     background-color: #1a1a1a;
    }

    input[type="search"] {
        border: none;
        background: transparent;
        margin: 0;
        padding: 7px 8px;
        font-size: 14px;
        color: inherit;
        border: 1px solid transparent;
        border-radius: inherit;
    }

    input[type="search"]::placeholder {
        color: #929292;
    }

    button {
        overflow: hidden;
        width: 40px;
        padding: 0;
        margin: 0;
        border: 1px solid transparent;
        border-radius: inherit;
        background: transparent url(/src/assets/searchIcon.svg) no-repeat center;
        cursor: pointer;
        opacity: 0.7;
    }
</style>
