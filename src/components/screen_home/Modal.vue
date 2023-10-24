<script setup>
import { ref } from "vue"


let categoria = ref(null)

const props = defineProps({
    categories: Object,
    categoria: String,
    showAlert: Boolean,
    play: Function,
    home: Function,


})


</script>


<template>

     <div class="modal fade " id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true" data-bs-backdrop="static" data-bs-keyboard="false">

    
        <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content colorModal">

            <div class="modal-body">
            <div class="row m-0 p-0 justify-content-center">
                <div class="col-12">
                <h5 class="text-center">Selecciona una categoria</h5>
                </div>
                <div class="col-12 my-4">
                <button v-for="(category, index) in Object.keys(categories)" :key="index" @click="categoria = category"
                    :class="categoria == category ? 'text-uppercase btn btn-primary m-1 btnCategoria' : 'text-uppercase btn btn-primary m-1'">{{
                    category }}</button>
                </div>


                <div class="col-12">
                <button type="button" class="btn btn-Cerrar" data-bs-dismiss="modal"
                    @click="categoria = null ; home()">CERRAR</button>
                <button type="button" class="btn btn-Jugar" :data-bs-dismiss="categoria ? 'modal' : ''"
                    @click="play(categoria)">JUGAR</button>
                </div>


                <div class="alert alert-danger mt-3 w-75" v-show="showAlert">
                <span>Por favor seleccione una categoria</span>
                </div>

            </div>
            </div>
        </div>
        </div>
        </div>  

</template>





<style>

/* Modal */
.colorModal {
  background-color: rgba(0, 0, 0, 0.87);
  color: rgb(255, 255, 255);
  border: 1px solid rgba(255, 255, 255, 0.527);
}



.btn-Cerrar {
  background-color: rgba(211, 8, 8, 0.815);
  border: 1px solid rgb(255, 0, 0);
  color: rgb(255, 255, 255);
  font-weight: 600;
  width: 100px;
  margin-right: 10px;
}

.btn-Cerrar:hover {
  background-color: rgb(255, 0, 0);
  border: 1px solid rgb(255, 0, 0);
  color: rgb(255, 255, 255);
  font-weight: 600;
  width: 100px;
  margin-right: 10px;
}


.btn-Jugar {
  background-color: rgb(0, 124, 0);
  border: 1px solid rgb(0, 255, 0);
  color: rgb(255, 255, 255);
  font-weight: 600;
  width: 100px;
  margin-left: 10px;
}

.btn-Jugar:hover {
  background-color: rgb(0, 97, 0);
  border: 1px solid rgb(0, 255, 0);
  color: rgb(255, 255, 255);
  font-weight: 600;
  width: 100px;
  margin-left: 10px;
}


.btnCategoria {
  background-color: rgb(165, 0, 0);
  border: 1px solid rgb(255, 255, 255);
  color: rgb(255, 255, 255);

}

.btnCategoria:hover {
  background-color: rgb(165, 0, 0);
  border: 1px solid rgb(255, 255, 255);
  color: rgb(255, 255, 255);
}

</style>