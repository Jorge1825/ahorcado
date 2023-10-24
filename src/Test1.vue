
<script setup>


const props = defineProps({
  iniciarJuego: Function,
});

</script>


<template>
  <button @click="iniciarJuego('nueva')">Iniciar Juego</button>
</template>

