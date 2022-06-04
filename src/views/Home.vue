<script setup>
import { defineEmits, reactive, computed, onMounted, watch } from 'vue'
import Product from '../components/Product.vue'
import { useToast } from 'vue-toastification'

const toast = useToast()
const emit = defineEmits('on-change-cart')
const products = reactive([
  {
    id: 1,
    name: 'Quần',
    price: 100
  },
  {
    id: 2,
    name: 'Áo',
    price: 200
  },
  {
    id: 3,
    name: 'Giày',
    price: 300
  },
  {
    id: 4,
    name: 'Dép',
    price: 500
  },
  {
    id: 5,
    name: 'Mũ',
    price: 350
  },
  {
    id: 6,
    name: 'Áo khoác',
    price: 1000
  }
])

const cart = reactive(JSON.parse(localStorage.getItem('list')) || [])

watch(cart, () => localStorage.setItem('list', JSON.stringify(cart)))

const handleAddProduct = (product) => {
  const indexProduct = cart.findIndex(p => p.id == product.id)
  if (indexProduct >= 0) {
    cart[indexProduct].number++;
  } else {
    cart.push({
      ...product,
      number: 1
    })
    emit('OnChangeCart', cart.length)
  }
  toast.success('Thêm giỏ hàng thành công')
}
</script>

<template>
  <div class="home">
    <div class="title">Feature Product</div>
    <div class="list">
      <Product
        v-for="product in products"
        :key="product.id"
        :name="product.name"
        :price="product.price"
        :id="product.id"
        @on-add-product="handleAddProduct(product)" />
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
.home .list {
  display: flex;
  flex-wrap: wrap;
  flex: 1 0 50%;
  justify-content: space-between;
}
</style>