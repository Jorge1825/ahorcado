<script setup>
  import {ref} from 'vue'
  import Test1 from './Test1.vue';
  
  categoria = ref(null)
  
  function miFuncion(categoria) {
    categoria.value = categoria
    console.log('hola', categoria);
  }
</script>

<template>
    <Test1 :iniciarJuego="miFuncion"/>
    
</template>
  
