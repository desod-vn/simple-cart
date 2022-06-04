<script setup>
import { defineProps, defineEmits, reactive} from 'vue'
import Trash from '../components/icons/Trash.vue'

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
  },
  number: {
    type: Number,
    default: 1,
  }
})

const product = reactive({
  number: props.number
})

const emit = defineEmits(['on-remove-product', 'on-change-number'])
</script>

<template>
  <div class="product-border">
    <img :src="props.image" alt="" />
    <div class="product-info">
      <div>
        <div class="product-name">
          {{ props.name }}
        </div>
        <div class="product-price">
          {{ props.price }} $
        </div>
      </div>
      <div class="product-calc">
        <div class="">
          <div class="product-name">
            Quantity
          </div>
          <input class="product-number" type="number" step="1" min="1" v-model="product.number" @change="$emit('on-change-number', {
            id: props.id,
            number: product.number
          })">
        </div>
        <div class="product-sub-total">
          <div class="product-name">
            Sub Total
          </div>
          <div class="product-price" style="text-align: center;">
            {{ product.number * props.price }} $
          </div>
        </div>
        <button class="product-add" @click="$emit('on-remove-product')">
          <Trash fill="black" height="25px" width="25px" />
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.product-border {
  display: flex;
  border: 1px solid #ddd;
  padding: 10px;
  margin: 15px 0;
}
.product-calc {
  display: flex;
}
.product-price {
  color: #D3455B;
  font-size: 30px;
}
.product-name {
  color: #000;
  font-size: 30px;
  line-height: 2;
}
.product-info {
  width: 100%;
  margin: 10px;
  display: flex;
  justify-content: space-between;
}
.product-add {
  height: 40px;
  color: #fff;
  padding: 3px 8px;
  border: 2px solid #ddd;
  background: transparent;
  align-self: center;
  outline: none;
  display: flex;
  align-items: center;
  border-radius: 5px;
}
.product-number {
  margin-right: 15px;
  padding: 8px;
  border-radius: 5px;
  border: 2px solid #ddd;
}
</style>