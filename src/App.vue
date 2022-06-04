<script setup>
import { reactive, computed } from 'vue'
import { RouterLink, RouterView } from 'vue-router'
import Header from './layouts/Header.vue'

const numberInCart = JSON.parse(localStorage.getItem('list')) || []
const cart= reactive({
  number: numberInCart.length
})

const handleIncreaseCart = (value) => {
  cart.number = value
}
</script>

<template>
  <Header
    :number="cart.number"
  />
  <RouterView
    @on-change-cart="handleIncreaseCart"
  />
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');

* {
  font-family: 'Roboto', sans-serif;
  padding: 0;
  margin: 0;
}
</style>