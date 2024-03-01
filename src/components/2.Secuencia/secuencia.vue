<template>
  
    <div>
      <div>
    <button v-if="!counting" @click="startCountdown">Empezar</button>
    <p v-if="intentos > 0">Intentos restantes: {{ intentos }}</p>
    <p v-else>No quedan intentos.</p>
    <div v-if="counting">
      <p>Te quedan: {{ countdown }} segundos</p>
    </div>
  </div>
      <h2>Completa la secuencia: </h2>
      <div>
        <button v-for="num in sequence" :key="num"  class="secuencia-button">
          {{ num === hiddenNumber ? '?' : num }}
        </button>
      </div>
      <div>
        Elige la opción correcta: <br>
        <button  class="option-button" v-for="option in options" :key="option" @click="checkOption(option)" >
          {{ option }}
        </button>
      </div>
      <div>
        <span>
            {{ Resultado }}
        </span>
      </div>
  
    
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        sequence: [],
        hiddenNumber: null,
        options: [],
        Resultado: '',
        intentos:2,
        counting: false,
        countdown: 10,
        timer: null // Declarar timer como una propiedad de datos
      };
    },
    mounted() {
      this.generateSequence();
    },
    methods: {
      startCountdown() {
       // Detener el temporizador existente si está en funcionamiento
        if (this.timer) {
          clearInterval(this.timer);
          this.timer = null;
        }
        
        //Aqui si los intentos son mayoires a 0 que empiece a generar una nueva secuencia y empiece el conteo
        if(this.intentos>0)
        {
        console.log(this.intentos)
        this.intentos--;
        console.log(this.intentos)
        this.countdown = 10;
        this.Resultado = ''; //reiniciamos el valor de nuestro resultado cuando le damos click
        this.generateSequence(); //genberamos una nueva secuencia
        this.counting = true;
     
        this.timer = setInterval(() => {
          if ((this.countdown > 0) && (this.intentos>=0)) {
            this.countdown--;
            console.log(this.intentos)
          } else {
            clearInterval(this.timer);
            this.counting = false;
            this.countdown = 10;
            //this.intentos--;
            this.Resultado = "¡Tiempo! El número oculto era:" + this.hiddenNumber;
          }
        }, 1000);
        }
    
      },
      generateSequence() {

        this.sequence = [];
        this.options = [];
        
        for (let numeros = 1; numeros <= 9; numeros++) {
          this.sequence.push(numeros);
        }
        this.sequence = this.sequence.sort(() => Math.random() - 0.5).slice(0, 8);
        this.hiddenNumber = this.sequence[Math.floor(Math.random() * this.sequence.length)];
        this.generateOptions();
        //this.intentos = 5; // Establecer intentos al inicio del juego
      },
      generateOptions() {
        this.options = this.sequence.filter(num => num !== this.hiddenNumber).slice(0, 2);
        this.options.push(this.hiddenNumber);
        this.shuffleArray(this.options);
      },
      checkOption(option) {
        

        if (this.counting) {
          clearInterval(this.timer);
          this.counting = false;
        }
        if (option === this.hiddenNumber) {
          //console.log('¡Correcto! El número oculto era:', this.hiddenNumber);
          this.Resultado = "¡Correcto! El número oculto era:" + this.hiddenNumber;
        } else {
          //this.intentos--;
          //console.log('Incorrecto. Inténtalo de nuevo.');
          this.Resultado = "Incorrecto El número oculto era:" + this.hiddenNumber;
        }
        //this.intentos--; // Decrementar intentos
      },
      shuffleArray(array) {
        for (let i = array.length - 1; i > 0; i--) {
          const j = Math.floor(Math.random() * (i + 1));
          [array[i], array[j]] = [array[j], array[i]];
        }
      }
    }
  };
  </script>

<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
.secuencia-button {
  margin: 5px;
  padding: 10px;
  background-color: #f0f0f0;
  border: 1px solid rgb(16, 209, 48);
  border-radius: 5px;
  cursor: pointer;
  transition: transform 0.3s ease;
}
.option-button {
  margin: 5px;
  padding: 10px;
  background-color: #f0f0f0;
  border: 1px solid rgb(117, 93, 93);
  border-radius: 5px;
  cursor: pointer;
  transition: transform 0.3s ease;
}
.option-button:hover {
  transform: scale(1.1);
}
</style>