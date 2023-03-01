<template>
  <h1>{{ name }}</h1>

  <input type="text" v-model="name" />

  <button @click="placeOrder">Place Order</button>
  <button @click="removeWatcher">Hide cart alert</button>

  <br />

  <label for="currencySymbol">Currency</label>
  <select id="currencySymbol" v-model="currencySymbol">
    <option value="$">$</option>
    <option value="€">€</option>
    <option value="£">£</option>
  </select>

  <YummyMealVue
    v-for="meal in meals"
    :key="meal.name"
    :name="meal.name"
    :price="meal.price"
    @addToCart="addItemToCart"
  />
</template>

<script setup>
import { ref, reactive, watch, provide, onMounted } from "vue";

import YummyMealVue from "./components/YummyMeal.vue";

const currencySymbol = ref("$");
provide("currencySymbol", currencySymbol);
const name = ref("Haska Sambuka");
const cart = reactive([]);
const meal = reactive({ name: "Sumbuka 🍸", price: 5 });
const meals = reactive([
  { name: "Sumbuka 🍸", price: 5 },
  { name: "Viski 🥃", price: 10 },
  { name: "Bloody Mary 🍹", price: 15 },
]);
const placeOrder = () => alert("Your order has been placed");
const addItemToCart = (item) => cart.push(item);

const removeWatcher = watch([() => [...cart]], (newCart, oldCart) => {
  alert(newCart.join("\n"));
});

onMounted(() => {
  console.log(name.value);
});
</script>
