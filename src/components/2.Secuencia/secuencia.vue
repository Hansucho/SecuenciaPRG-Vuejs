<template>
    <div>
      <h2>Completa la secuencia: </h2>
      <div>
        <button v-for="num in sequence" :key="num"  class="secuencia-button">
          {{ num === hiddenNumber ? '?' : num }}
        </button>
      </div>
      <div>
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
        sequence: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
        hiddenNumber: null,
        options: [],
        Resultado:'' // Opciones aleatorias
      };
    },
    mounted() {
      this.hiddenNumber = this.sequence[Math.floor(Math.random() * this.sequence.length)];
      this.generateOptions();
    },
    methods: {
      generateOptions() {
        // Generar opciones aleatorias basadas en la secuencia, excluyendo el número oculto
        this.options = this.sequence.filter(num => num !== this.hiddenNumber).slice(0, 2); // Por ejemplo, mostraremos solo dos opciones
        this.options.push(this.hiddenNumber); // Agregar el número oculto a las opciones
        this.shuffleArray(this.options); // Mezclar las opciones
      },
      checkOption(option) {
        if (option === this.hiddenNumber) {
          console.log('¡Correcto! El número oculto era:', this.hiddenNumber);
          this.Resultado="¡Correcto! El número oculto era:" + this.hiddenNumber
          // Lógica adicional si la opción seleccionada es correcta
        } else {
          console.log('Incorrecto. Inténtalo de nuevo.');
          this.Resultado="Incorrecto El número oculto era:" + this.hiddenNumber
          // Lógica adicional si la opción seleccionada es incorrecta
        }
      },
      shuffleArray(array) {
        // Función para mezclar un array
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