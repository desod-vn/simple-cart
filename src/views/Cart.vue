<script setup>
import { defineEmits, reactive, computed, onMounted, watch } from 'vue'
import ProductCart from '../components/ProductCart.vue'
import { useToast } from 'vue-toastification'

const toast = useToast()
const emit = defineEmits('on-change-cart')

const cart = reactive(JSON.parse(localStorage.getItem('list')))

watch(cart, () => localStorage.setItem('list', JSON.stringify(cart)))

const handleRemoveProduct = (product) => {
  const indexProduct = cart.findIndex(p => p.id == product.id)
  if (indexProduct >= 0) {
    cart.splice(indexProduct, 1);
    emit('OnChangeCart', cart.length)
  }
  toast.warning('Xoá giỏ hàng thành công')
}

const handleChangeNumber = (product) => {
  const indexProduct = cart.findIndex(p => p.id == product.id)
  if (indexProduct >= 0) {
    cart[indexProduct].number = product.number;
  }
}

const sum = cart => {
  let result = 0
  for(let i = 0; i < cart.length; i++) {
    result += cart[i].number * cart[i].price
  }
  return result
}
</script>

<template>
  <div class="home">
    <div class="title">Feature Product</div>
    <div style="text-align: right;">
      <button class="product-add">
        Check out
      </button>
    </div>
    <div class="list">
      <ProductCart
        v-for="product in cart"
        :key="product.id"
        :name="product.name"
        :price="product.price"
        :number="product.number"
        :id="product.id"
        @on-change-number="handleChangeNumber"
        @on-remove-product="handleRemoveProduct(product)"
      />
    </div>
    <div class="cart-total">
      Total {{ sum(cart) }} $
    </div>
    <div style="text-align: right;">
      <button class="product-add">
        Check out
      </button>
    </div>
  </div>
</template>

<style scoped>
.home {
  margin: 5% 15%;
}
.home .title {
  font-size: 25px;
  text-align: center;
}
.cart-total {
  text-align: right;
  margin: 20px;
  font-size: 30px;
  font-weight: bold;
}
.product-add {
  color: #fff;
  padding: 10px 40px;
  border: none;
  outline: none;
  font-size: 18px;
  background: #6558F5;
  display: inline-block;
  border-radius: 5px;
}
</style>