<!-- <script setup>
import { ref, computed } from 'vue';

const counter = ref(0);
const color = ref('yellow')

const sumarUno = () => {
  counter.value++;
  //colorResultado();
}

const restarUno = () => {
  counter.value--;
  //colorResultado();
}

const reset = () => {
  counter.value = 0;
  //colorResultado();
}

//Manera de fer correcte, però n'hi ha de més òptimes

// function colorResultado() {
//   if (counter.value > 0) {
//     return color.value = 'green';

//   } else if (counter.value < 0) {
//     return color.value = 'red';

//   } else {
//     return color.value = 'yellow';
//   }
// }

//Manera de fer amb el Computed

const classCounter = computed(() => {
  if (counter.value === 0) {
    return 'zero';

  } else if (counter.value > 0) {
    return 'positive';

  } else {
    return 'negative';
  }
})

</script>

<template>
  <h1>Contador</h1>
  <button v-on:click="sumarUno">Sumar</button>
  <button v-on:click="restarUno">Restar</button>
  <button v-on:click="reset">Reset</button>
  Manera de fer amb computed -->
  <!-- <h3 :class="classCounter">{{ counter }}</h3>
</template>

<style>
button {
  margin: 1rem;
}

.positive {
  color: green;
}

.negative {
  color: red;
}

.zero {
  color: peru;
}
</style> -->


<script setup>
import { ref, computed } from 'vue';
const contador = ref(0);
const color = ref('yellow');
const arrayNum = ref([]);



const sumar = () => {
  contador.value++;
  definirColor();
  
}

const restar = () => {
  contador.value--;
  definirColor();
  
  
}

const reset = () => {
  contador.value = 0;
  definirColor();
  
  
}

const btnActivo = computed(()=>{
  const contieneNum = arrayNum.value.includes(contador.value);
  // if(contieneNum){
  //   return true
  // } else {
  //   return false
  // }

  //El mateix que el condicional anterior, però amb ternari
  return contieneNum ? true : false;
})

const agregar = () => {
  arrayNum.value.push(contador.value);
}

const definirColor = () => {
  if (contador.value > 0) {
    return color.value = 'green';


  } else if (contador.value < 0) {
    return color.value = 'red';


  } else {
    return color.value = 'yellow';
  }
}


//Se puede hacer definiendo una función o como una expresión directamente en la clase...
const definirClass = computed(() => {
  if (contador.value > 0) {
    return 'positive';

  } else if (contador.value < 0) {
    return 'negative';

  } else {
    return 'neutral'
  }
})

</script>




<template>
  <h1>Contador</h1>
  <h2 :style="`color:${color};`">{{ contador }}</h2>
  <button v-on:click="sumar">Sumar</button>
  <button v-on:click="restar">Restar</button>
  <button v-on:click="reset">Reset</button>
  <button :disabled="btnActivo" v-on:click="agregar">Add</button>

  <!-- Manera con una expresión de js en la misma clase -->
  <!-- <h2 :class=" contador >= 0 ? 'positive' : 'negative'">{{ contador }}</h2> -->

  <!-- Manera con el computed(más optimizada).Hace lo mismo que la línea 156 -->
  <h2 :class="definirClass">{{ contador }}</h2>

  <ul>
    <li v-for="(num, index) in arrayNum" :key="index">
      {{ num }}
    </li>
  </ul>
  
  <!-- <h3>{{ arrayNum }}</h3> -->
</template>



<style>
button {
  margin: 0.5rem;
}

.positive {
  color: green;
}

.negative {
  color: red;
}

.neutral {
  color: yellow;
}
</style>

