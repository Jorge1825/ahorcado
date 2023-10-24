<script setup>
import Home from './components/screen_home/Home.vue'
import Swal from 'sweetalert2/dist/sweetalert2.js'
import Confetti from 'vue-confetti/src/confetti.js';

import Modal from './components/screen_home/Modal.vue'
// mostrar alerta de SweetAlert2 de derrota
let gameOver = () => {
    soundPerder.play()
  Swal.fire({
      title: 'Perdiste',
      padding: '0 0 10px 0',
      icon: 'error',
      background: 'rgb(0, 3, 15, 1)',
      color: 'white',
      confirmButtonText: 'Volver a jugar',
      confirmButtonColor: 'rgb(25, 97, 230)',
      allowOutsideClick: false,
      allowEscapeKey: false,

      showClass: {
        popup: 'animate__animated animate__fadeInDown'
      },
      hideClass: {
        popup: 'animate__animated animate__fadeOutUp'
      },
      width: 400,
      //color al borde del Swal
      customClass: {
        popup: 'border border-light',

      },
      didOpen: () => {
        Swal.getConfirmButton().setAttribute('data-bs-toggle', 'modal')
        Swal.getConfirmButton().setAttribute('data-bs-target', '#exampleModal')

      }
    })
}
import Keyboard from './components/screen_home/Keyboard.vue'
import Temp from './components/Temp.vue'

import { ref,onMounted } from 'vue'





    // confetti
    const confetti = ref(null);

    const startConfetti = () => {
      confetti.value.start({
        colors: ['#FF6F61', '#004C83', '#55C6A9', '#FFC82B']
      });
      setTimeout(() => {
        confetti.value.stop();
      }, 4000);
    };

    onMounted(() => {
      confetti.value = new Confetti();
    });


    
    // teclado 
    let letters = ref(['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'])
    
    
    // categorias
    const categories = ref({
      colors: ['amarillo', 'verde', 'morado', 'azul', 'blanco'],
      animals: ['leon', 'loro', 'avetruz', 'puma', 'mono'],
      names: ['juan', 'jorge', 'andres'],
      countries: ['mexico', 'colombia', 'argentina', 'peru', 'chile'],
    })

    const images = [
      '../src/assets/img/1.png',
      '../src/assets/img/2.png',
      '../src/assets/img/3.png',
      '../src/assets/img/4.png',
      '../src/assets/img/5.png',
      '../src/assets/img/6.png',
    ]


    //sonidos del juego
    const sounds = [
      '../src/assets/sounds/click.mp3',
      '../src/assets/sounds/entrar.mp3',
      '../src/assets/sounds/ganar.mp3',
      '../src/assets/sounds/peligro.mp3',
      '../src/assets/sounds/perder.mp3',
    ]

    const soundPerder = new Audio(sounds[4])
    const soundGanar = new Audio(sounds[2])
    const soundClick = new Audio(sounds[0])
    const soundEntrar = new Audio(sounds[1])
    const soundPeligro = new Audio(sounds[3])
    

    let categoria = ref(null)

    // modal error
    let showAlert = ref(false)
    let imageAhorcado = ref('../src/assets/img/1px.png')

    let isPlaying = ref(false)
    let word = ref(null)

    let letterCorrect = ref('')
    let letterIncorrect = ref('')


    // mostrar alerta de SweetAlert2 de victoria
    let winner = () => {
        soundGanar.play()
      Swal.fire({
          title: 'Felicitaciones',
          padding: '0 0 10px 0',
          icon: 'success',
          background: 'rgb(0, 3, 15, 1)',
          color: 'white',
          confirmButtonText: 'Volver a jugar',
          confirmButtonColor: 'rgb(25, 97, 230)',
          allowOutsideClick: false,
          allowEscapeKey: false,
          showClass: {
            popup: 'animate__animated animate__fadeInDown'
          },
          hideClass: {
            popup: 'animate__animated animate__fadeOutUp'
          },
          width: 400,
          //color al borde del Swal
          customClass: {
            popup: 'border border-light',
          },
          //agregar  data-bs-toggle="modal" data-bs-target="#exampleModal" @click="reset()" al boton de confirmacion y cerrar el swal
          didOpen: () => {
            Swal.getConfirmButton().setAttribute('data-bs-toggle', 'modal')
            Swal.getConfirmButton().setAttribute('data-bs-target', '#exampleModal')
          }
        })
        startConfetti()
    }



    //setear varibales
     const reset = () => {
      console.log('reset')
      word.value = ''
      letterCorrect.value = ''
      letterIncorrect.value = ''
      imageAhorcado.value = '../src/assets/img/1px.png'
    }


    //funcion para retornar a la pantalla de inicio
    const retornHome = ()=> {
      isPlaying.value = false
      reset()
    }



    //funcion para validar que se seleccione una categoria
    const validarCategoria = ()=> {
      soundGanar.pause()
      soundPerder.pause()
      reset()
      console.log(categoria.value);

      if (!categoria.value) {
        showAlert.value = true

        setTimeout(() => {
          showAlert.value = false
        }, 3000)
      } else {
        return true
      }
    }



    //funcion para iniciar el juego
    const iniciarJuego = (cate)=> {
      categoria.value = cate

        soundGanar.pause()
        soundPerder.pause()
        soundEntrar.play()
        console.log(validarCategoria())
      if (validarCategoria()) {
        console.log(categoria.value)
        console.log('todo listo para jugar')
        isPlaying.value = true
        

        //selecionar una palabra aleatoria de la categoria elegida incluyendo la primera y ultima de la lista 
        let number = Math.floor(Math.random() * categories.value[categoria.value].length)

        word.value = categories.value[categoria.value][number]
        console.log(word.value)

        console.log('todo listo para jugar')
      }

    }





    //funcion para validar si la letra esta en la palabra 
    function letraRepetidaEnPalabra(letra) {
        const caracteres = word.value.split('');
        // Buscar cuantas veces se repite la letra en la palabra
        const caracteresRepetidos = caracteres.filter(caracter => caracter === letra);
   
        return caracteresRepetidos.length ;
    }


    //funcion ejecutada al presionar algún boton del teclado
    const input = (letter)=> {
        soundEntrar.pause()
        soundClick.play()

        console.log(letter)
            


            if (word.value.includes(letter) && !letterCorrect.value.includes(letter)) {

                for (let i = 0; i < letraRepetidaEnPalabra(letter); i++) {
                    letterCorrect.value += letter
                }
                if (letterCorrect.value.length == word.value.length) {
                    console.log('ganaste')
                    //alerta de felicitaciones
                    winner()
                    }

            } else {
                letterIncorrect.value += letter
                imageAhorcado.value = images[letterIncorrect.value.length - 1]

                if (letterIncorrect.value.length == images.length - 1) {
                    console.log('cuidado')
                        soundPeligro.play()
                }

                if (letterIncorrect.value.length == images.length) {
                    console.log('perdiste')
                    gameOver()
                }
            }

        }


  
</script>





<template>
  <div class="title">El ahorcado</div>

  <template v-if="isPlaying">
    <div class="row m-0 p-0 cuerpo align-content-center">
      <!-- juego img palabra -->
      <Temp :word="word" :letterCorrect="letterCorrect" :letterIncorrect="letterIncorrect" :imageAhorcado="imageAhorcado" />
      
    </div>

    <div class="row my-3 p-0 m-0 justify-content-center d-flex keyboard ">
      
      <!-- Keyboard -->
      <keyboard :input="input" :letters="letters" />

    </div>

  </template>


  <!-- Ventana de bienvenida -->
  <template v-else>
    <Home />
  </template>

  <!-- Modal -->
    <Modal :categories="categories" :categoria="categoria"  :showAlert="showAlert" :play="iniciarJuego" :home="retornHome" />

</template>





<style>
.title {

  top: 0;
  left: 0;
  width: 100%;
  background-color: rgba(32, 32, 32, 0.418);
  border-radius: 10px;
  font-size: 30px;
  font-weight: 600;
  padding: 10px;
}

.cuerpo {
  top: 50%;
  left: 0;
  width: 100%;
  height: 100%;
  margin-top: -50px;
  /* la mitad de la altura */
}

/* Keyboard */

.keyboard {
  bottom: 0;
  left: 0;
  width: 100%;
  text-align: center;

}


</style>
