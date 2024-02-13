<script setup>
import {ref, computed} from 'vue';

const name = "Marino";
const theme = {
  color : 'yellow'
};

const styleColor = "color: red";
const arrayColores = ["red", "blue", "orange"];
const active = true;

const arrayFrutas = [
  {
    name: "Manzana",
    price: "$2500",
    description: "Frutas exoticas rojas",
    stock: 10
  },
  {
    name: "Mango",
    price: "$5500",
    description: "Frutas dulces",
    stock: 50
  },
  {
    name: "Pera",
    price: "$3500",
    description: "Frutas de fibra",
    stock: 19
  },
  {
    name: "Melón",
    price: "$2000",
    description: "Frutas colombianas",
    stock: 20
  },
];

  //Metodos
  const handleClick = () => {
    console.log("Me diste un click")
  }

  const counter = ref(0); 
  const classCounter = computed(() => {
    if (counter.value == 0) {
      return 'indiferent'
    }

    if (counter.value > 0) {
      return 'positive'
    }

    if (counter.value < 0) {
      return 'negative'
    }
    
  });

  const increment = () => {    
    counter.value++;
  }

  const decrement = () => {    
    counter.value--;
  }

  const reset = () => {    
    counter.value = 0;
  }

  const arrayFavoritos = ref([]);

  const addFavorite = () => {
    arrayFavoritos.value.push(counter.value);
  }

  const bloquearBtnAdd = computed(() => {
    const numSearch = arrayFavoritos.value.find(numb => numb === counter.value);
    return numSearch ? true : false;
  })
  

</script>

<template>
  <h1>Hola {{ name.toUpperCase() }} :)</h1>
  <h2 :style="styleColor">Hola mundo desde Vue Js</h2>

  <h2 :style="`color: ${arrayColores[2]}`">Soy Colombia</h2>
  <h2 v-if="active">Estoy activo</h2>
  <p v-else>Estoy inactivo</p>
  <h2>Frutas</h2>
  <ul>
    <li v-for="(fruta, index) in arrayFrutas" :key="index"> 
      <span v-if="fruta.stock > 0">
        {{ fruta.name }} {{ fruta.price }} {{ fruta.stock }}
      </span>
    </li>
  </ul>

  <button v-on:click.right.prevent="handleClick">Activame right</button>
  <button @click="handleClick">Activame left</button>
  <button @click.middle="handleClick">Activame middle</button>

  <hr>
  <h2>Armando un contador reactivo</h2>
  <h1 :class="classCounter">{{ counter }}</h1>

  <button @click="increment">Aumentar</button>
  <button @click="decrement">Disminuir</button>
  <button @click="reset">Resetear</button>
  <button :disabled="bloquearBtnAdd" @click="addFavorite">Add</button>

  <ul><li v-for="favorite in arrayFavoritos">
    {{ favorite }}
  </li></ul>

</template>

<style>
h1 {
  color: v-bind('theme.color');
}

.positive {
  color: green;
}

.negative {
  color: red;
}

.indiferent {
  color: black;
}
</style>
