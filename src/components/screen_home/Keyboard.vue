<script setup>
import { ref } from "vue"


const props = defineProps({
    letters: Array,
    input: Function,


})


</script>


<template>

<div class="col-12 col-md-8 col-xl-10  p-0 m-0">
        <div class="row d-flex justify-content-center mx-0 px-0 ">
          <template v-for="(letter, index) in letters" :key="index">
            <button class="col-1 p-0 btn btnLetter py-2 text-center" 
              @click="input(letter)" >{{ letter }}</button>
          </template>

        </div>
      </div>

</template>





<style>
.btnLetter {
  background-color: rgb(255, 255, 255);
  color: rgb(0, 0, 0);
  border: 1px solid rgb(0, 0, 0);
  cursor: pointer;
  font-size: 1.2rem;
  font-weight: 600;
  text-transform: uppercase;
  margin: 3px;
}

.btnLetter:hover {
  background-color: rgb(0, 0, 0);
  color: rgb(255, 255, 255) !important;
  border: 1px solid rgb(255, 255, 255);
  cursor: pointer;
  font-size: 1.2rem;
  font-weight: 600;
  text-transform: uppercase;
  margin: 3px;
}
</style>