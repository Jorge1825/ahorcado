<template>
        <div class="row m-0 p-0 body">
            <div class="col-md-10 col-12 col-lg-7 msgB">
                <div class="row">
                    <div class="col-12">
                        <h2 class="text-center">Bienvenido al juego del ahorcado</h2>
                        <p class="text-lowercase"><span class="text-uppercase">E</span>ste juego consiste en adivinar la palabra que se muestra en pantalla, para ello
                            deberas presionar las letras que creas que estan en la palabra, si aciertas la letra se
                            mostrara en la pantalla, si no aciertas la letra se mostrara una parte del ahorcado, si no
                            aciertas la palabra antes de que se complete el ahorcado perderas el juego.</p>
                    
                    
                        </div>
                    <div class="col-12 my-3 justify-content-center d-flex ">
                        <img class="imgB" src="../screen_home/img/IMG_BIENVENIDA.jpg" alt="imagen del ahorcado">
                    </div>
                    <div class="col-12 mt-3">
                        <p class="text-center fw-bold">Presiona el boton para comenzar</p>
                    </div>
                    <div class="col-12 justify-content-center d-flex">
                        <button class="btn btn-primary fw-bold" data-bs-toggle="modal" data-bs-target="#exampleModal">Comenzar</button>
                    </div>
                </div>

            </div>
        </div>
</template>

<script>
export default {
    components: {
        // HelloWorld
    },
    setup() {
        // const msg = ref('Hello World')
        return {
        //   msg
        }
    }
    
}
</script>

<style>

.body {
    height: 90%;
    width: 100%;
    justify-content: center;
    align-items: center;
    display: flex;
}


.msgB {
    font-size: 17px;
    font-weight: 600;
    color: rgb(255, 255, 255);
    background-color: rgba(0, 0, 0, 0.418);
    padding: 20px;
    border-radius: 10px;
    text-align: justify;
}

.imgB {
    width: 30%;
    height: 100%;
    border-radius: 10px;
}
</style>