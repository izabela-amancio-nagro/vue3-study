<template>
  <div v-if="data && data.length > 0" class="container">
    <section>
      <img :src="currentProduct.image" />
    </section>
    <section class="column">
      <h1>{{ currentProduct.name }}</h1>
      <p>{{ currentProduct.description }}</p>
      <a :href="link">Made by Shop</a>
      <p v-if="currentProduct.onSale" class="on-sale">On sale!</p>
      <p>Colors:</p>
      <div
        v-for="color in colors"
        :key="color"
        :class="color === 'green' ? 'color-green' : 'color-blue'"
        @mouseover="updateImage(color)"
        @mouseout="resetImage"
      ></div>
      <ul>
        <p>Available sizes:</p>
        <li v-for="size in currentProduct.sizes" :key="size">{{ size }}</li>
      </ul>

      <button class="btn" @click="addToCart">Add to cart</button>
    </section>
    <div class="column">
      <p class="cart">Cart: ({{ cart }})</p>

      <div class="icon mdi mdi-trash-can-outline" @click="removeFromCart">
        <span>Remove</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'

const data = ref([])
const currentProduct = ref(null)
const link = 'https://example.com' // Defina seu link aqui
const cart = ref(0) // Seu contador de carrinho
const colors = ['green', 'blue']

const products = [
  {
    id: '111',
    name: 'Funny Green Socks',
    description: 'Crazy and funny pair of green socks.',
    color: 'green',
    sizes: ['P', 'M', 'L', 'XL'],
    image: '../src/assets/socks_green.jpg',
    onSale: true // Exemplo de produto em promoção
  },
  {
    id: '222',
    name: 'Mysterious Blue Socks',
    description: 'Magic and mysterious pair of blue socks.',
    color: 'blue',
    sizes: ['M', 'L'],
    image: '../src/assets/socks_blue.jpg',
    onSale: false // Exemplo de produto não em promoção
  }
]

const defaultImage = '../src/assets/socks_green.jpg'

const updateImage = (color) => {
  currentProduct.value.image = products.find((product) => product.color === color).image
  currentProduct.value.name = products.find((product) => product.color === color).name
}
const resetImage = () => {
  currentProduct.value.image = defaultImage
}

const addToCart = () => {
  cart.value += 1
}

const removeFromCart = () => {
  cart.value -= 1
}

onMounted(() => {
  data.value = products
  currentProduct.value = products[0] // Definindo o primeiro produto como produto atual
})
</script>

<style scoped>
.container {
  display: flex;
}

img {
  width: 350px;
  height: 350px;
}

h1 {
  font-size: 36px;
  font-weight: 700;
}

.column {
  flex: 1;
  padding: 20px;
}

.on-sale {
  max-width: 100px;
  font-size: 18px;
  font-weight: 700;
  text-align: center;
  color: red;
  background-color: blanchedalmond;
  padding: 4px;
}

.btn {
  margin-top: 16px;
  padding: 20px 80px;
  background: black;
  font-size: 14px;
  font-weight: 600;
  text-transform: uppercase;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.cart {
  width: 100px;
  height: 30px;
  border: 2px solid #ccc;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
}

.icon {
  display: flex;
  align-items: center;
  font-size: 18px;
  color: red;
  cursor: pointer;
}

.icon > span {
  margin-left: 4px;
  color: black;
  font-size: 14px;
  font-weight: 500;
}

.color-green {
  width: 50px;
  height: 50px;
  background: #0fce3c;
  border: 2px solid #ccc;
  border-radius: 50%;
}

.color-blue {
  width: 50px;
  height: 50px;
  background: #220e83;
  border: 2px solid #ccc;
  border-radius: 50%;
}
</style>
