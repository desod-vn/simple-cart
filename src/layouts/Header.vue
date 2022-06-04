<script setup>
import Cart from '../components/icons/Cart.vue'
const props = defineProps({
  number: {
    type: Number,
    default: 0
  }
})
</script>
<template>
  <div class="header">
    <div class="header-logo">
      SWIFTPOD
    </div>
    <div class="header-menu">
      <router-link :to="{ name: 'home' }">HOME</router-link>
      <router-link :to="{ name: 'home' }">PRODUCT</router-link>
      <router-link :to="{ name: 'cart' }">CART</router-link>
    </div>
    <div class="header-icon">
        <Cart />
        <div class="cart-number">{{ props.number }}</div>
    </div>
  </div>
</template>

<style>
.header {
  padding: 10px 20px 10px 30px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #F7F9FA;
  border-bottom: 1px solid #000;
  flex-wrap: nowrap;
}
.header-logo {
  flex: 33.33%;
  font-size: 30px;
  font-weight: bold;
}
.header-menu {
  flex: 33.33%;
  display: flex;
  gap: 50px;
  /* margin: 0 500px; */
  justify-content: center;
  align-items: center;
}
.header-menu a, .header-menu a:hover, .header-menu a:active, .header-menu a:visited {
  text-decoration: none;
  color: #000;
}
.header-icon {
  flex: 33.33%;
  text-align: right;
  position: relative;
}
.header-icon .cart-number {
  background: #E9A2AD;
  text-align: center;
  position: absolute;
  top: 0;
  color: #fff;
  right: 0;
  transform: translate(50%, -50%);
  height: 20px;
  width: 20px;
  border: 1px solid #D3455B;
  border-radius: 50%;
}
</style>