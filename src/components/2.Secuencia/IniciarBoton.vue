<template>
    <div class="text-center">
      <v-btn
        class="ma-2"
        outlined
        color="indigo"
        @click="Iniciar"
      >
       {{ texto }}
      </v-btn>
    
      <template>
        <v-card
          class="mx-auto my-12"
          max-width="374"
        >
        <template slot="progress">
      <v-progress-linear
        color="deep-purple"
        height="10"
        :value="countdown * 10"
        :indeterminate="!counting" 
        > </v-progress-linear>
    </template>

          <v-card-title>Bienvenido</v-card-title>

           <!--aqui indicamos el estatus del usuario-->
          <v-card-text>
            <!--aqui indicamos los intentos restantes-->
            <v-row
              align="center"
              class="mx-0"
            >

      
      <!-- Mostrar mensaje de intentos restantes y temporizador si está en conteo -->
      <div v-if="!counting">
        <p v-if="intentos > 0">Intentos restantes: {{ intentos }}</p>
        <p v-else>No quedan intentos.</p>
        <p>Te quedan: {{ countdown }} segundos</p>
        
      </div>
              
            </v-row>
           
           
          </v-card-text>
           <!--aqui indicamos el estatus del usuario-->

          <v-divider class="mx-4"></v-divider>


        </v-card>
      </template>

    </div>
    
  </template>

  

<script>
export default {
  props: {
    counting: Boolean,
    texto: String,
    intentos: Number,
    countdown: Number
  },
  data() {
    return {
      loading: false,
      ratingValue: 5,
      //counting:false // Valor inicial de la calificación
    };
  },
  methods: {
    Iniciar() {
      this.$emit('Iniciar');
    },
    handleRatingInput(value) {
      if (!this.counting) {
        this.ratingValue = value;
      }
    }
  }
};
</script>