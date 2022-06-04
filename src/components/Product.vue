<script setup>
import { defineProps, defineEmits} from 'vue'
import Cart from '../components/icons/Cart.vue'

const props = defineProps({
  id: {
    type: Number,
  },
  image: {
    type: String,
    default: 'https://picsum.photos/350/200'
  },
  name: {
    type: String,
    default: 'Sample Product'
  },
  price: {
    type: Number,
    default: 100
  }
})

const emit = defineEmits(['on-add-product'])
</script>

<template>
  <div class="product-border">
    <img :src="props.image" alt="" />
    <div class="product-info">
      <div>
        <div class="product-price">
          {{ props.price }} $
        </div>
        <div class="product-name">
          {{ props.name }}
        </div>
      </div>
      <button class="product-add" @click="$emit('on-add-product')">
        <Cart fill="white" height="25px" width="25px" /> Add
      </button>
    </div>
  </div>
</template>

<style scoped>
.product-border {
  width: 350px;
  border: 1px solid #ddd;
  padding: 10px;
  margin: 15px 0;
}
.product-price {
  color: #D3455B;
}
.product-name {
  color: #000;
  line-height: 2;
}
.product-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.product-add {
  color: #fff;
  padding: 3px 8px;
  border: none;
  outline: none;
  background: #6558F5;
  display: flex;
  align-items: center;
  gap: 10px;
  border-radius: 5px;
}
</style>