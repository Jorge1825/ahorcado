<template>
    <div class="col-12">
        <div class="row p-0 m-0 justify-content-between d-flex">
            <div class=" col-md-6 col-12 justify-content-center align-items-center d-flex">
                <div class="" v-for="(letter, index) in word" :key="index">
                    <h2 class="pb-md-5 pb-sm-5 text-uppercase letter " v-text="letterCorrect.includes(letter) ? letter : ''"
                        :style="letterCorrect.includes(letter) ? 'border-bottom: none;' : ''"></h2>
                </div>
            </div>
            <div class="col-md-6 mt-4 mt-md-0 col-12 justify-content-center d-flex">
                <div class="game_display_image">
                    <img class="imageAhorcado" :src='imageAhorcado'>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
const props = defineProps({
    word: String,
    letterCorrect: String,
    letterIncorect: String,
    imageAhorcado: String
})
</script>

<style>
.letter {
    color: rgb(255, 255, 255);
    border-bottom: 2px solid rgb(255, 255, 255);
    cursor: pointer;
    margin: 5px;
    width: 5vw;
    height: 5vh;
    text-align: center;
    line-height: 50px;
    font-size: 4.8vw;
    font-weight: 600;
}

.imageAhorcado {
    height: 18rem;
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
}

/* imagen del fondo del ahorcado */
/* ./assets/img/fondo.png */
.game_display_image {
    width: 100%;
    height: 18rem;
    background-image: url('../assets/img/fondo.png');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
}
</style>