<script setup>
import { ref, computed } from "vue";
import CourseCard from "./components/CourseCard.vue";

const courses = ref([
  {
    id: 1,
    name: "Italian Cooking",
    price: 499,
    soldOut: false,
  },
  {
    id: 2,
    name: "Baking Basics",
    price: 399,
    soldOut: false,
  },
  {
    id: 3,
    name: "Sushi Masterclass",
    price: 699,
    soldOut: true,
  },
]);

const cart = ref([]);

function addToCart(course) {
  const existingItem = cart.value.find((item) => item.id === course.id);

  if (existingItem) {
    existingItem.quantity++;
  } else {
    cart.value.push({
      id: course.id,
      name: course.name,
      price: course.price,
      quantity: 1,
    });
  }
}

function increaseQuantity(id) {
  const item = cart.value.find((item) => item.id === id);

  if (item) {
    item.quantity++;
  }
}

function decreaseQuantity(id) {
  const item = cart.value.find((item) => item.id === id);

  if (item && item.quantity > 1) {
    item.quantity--;
  }
}

function removeItem(id) {
  cart.value = cart.value.filter((item) => item.id !== id);
}

const subtotal = computed(() => {
  return cart.value.reduce((total, item) => {
    return total + item.price * item.quantity;
  }, 0);
});

const tax = computed(() => {
  return subtotal.value * 0.15;
});

const grandTotal = computed(() => {
  return subtotal.value + tax.value;
});
</script>

<template>
  <h1>Cooking Masterclass Checkout</h1>
  <p>Browse cooking courses and build your cart.</p>

  <div class="container">
    <CourseCard
      v-for="course in courses"
      :key="course.id"
      :name="course.name"
      :price="course.price"
      :soldOut="course.soldOut"
      @add-to-cart="addToCart(course)"
    />
  </div>

  <h2>Cart</h2>

  <div v-for="item in cart" :key="item.id" class="cart-item">
    <p>{{ item.name }}</p>

    <button @click="decreaseQuantity(item.id)">-</button>

    <span>{{ item.quantity }}</span>

    <button @click="increaseQuantity(item.id)">+</button>

    <button @click="removeItem(item.id)">Remove</button>
  </div>

  <h2>Checkout Summary</h2>

  <p>Subtotal: R{{ subtotal.toFixed(2) }}</p>
  <p>Tax (15%): R{{ tax.toFixed(2) }}</p>
  <p>
    <strong>Total: R{{ grandTotal.toFixed(2) }}</strong>
  </p>
</template>

<style>
.container {
  display: flex;
  gap: 20px;
  justify-content: center;
  flex-wrap: wrap;
}

.cart {
  margin-top: 20px;
  text-align: center;
}

.cart-item {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  margin: 8px 0;
}
</style>
