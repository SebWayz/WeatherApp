<script setup lang="ts">
  import { ref, inject, reactive } from 'vue'

  const axios: any = inject('axios')

  const state = reactive({
    selectedCity: ref(''),
    inputError: false,
    inputErrorMsg: 'Le nom doit faire 2 caractères minimum.'
  });

  const emit = defineEmits<{
    (event: 'selectedCity', city: string): void
  }>();

  const submitCity = () => {
    state.inputError = false
    if (state.selectedCity.length >= 2) {
        emit('selectedCity', state.selectedCity)
        state.selectedCity = ''
    } else {
        state.inputError = true
    }
  }
</script>

<template>
    <div>
        <input v-model="state.selectedCity" type="search" placeholder="Nom de ville / village" name="rechercheVille" id="rechercheVille" ref="rechercheVille" @keyup.enter="submitCity">
        <button @click="submitCity"/>
    </div>

    <div v-if="state.inputError">
      <h2 style="color: #a3160b;">{{ state.inputErrorMsg }}</h2>
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
