<script setup>
import { ref } from "vue";

const wishlistCount = ref(0);

const savedCourses = ref([]);

const courses = ref([
  {
    id: 1,
    title: "Italian Pasta Mastery",
    chef: "Chef Marco",
    price: 499,
    level: "Beginner",
    available: true,
  },
  {
    id: 2,
    title: "French Pastry Basics",
    chef: "Chef Marie",
    price: 799,
    level: "Intermediate",
    available: false,
  },
  {
    id: 3,
    title: "Sushi Fundamentals",
    chef: "Chef Ken",
    price: 999,
    level: "Advanced",
    available: true,
  },
  {
    id: 4,
    title: "South African Braai Essentials",
    chef: "Chef Themba",
    price: 599,
    level: "Beginner",
    available: true,
  },
  {
    id: 5,
    title: "Artisan Bread Making",
    chef: "Chef Isabella",
    price: 899,
    level: "Intermediate",
    available: true,
  },
  {
    id: 6,
    title: "Thai Street Food Secrets",
    chef: "Chef Anong",
    price: 1099,
    level: "Advanced",
    available: false,
  },
]);

function saveCourse(courseId) {
  if (!savedCourses.value.includes(courseId)) {
    savedCourses.value.push(courseId);
    wishlistCount.value++;
  }
}
</script>

<template>
  <h1>🍳 Cooking Masterclass</h1>

  <p class="wishlist">Wishlist: {{ wishlistCount }}</p>

  <div class="container">
    <div v-for="course in courses" :key="course.id" class="card">
      <h2>{{ course.title }}</h2>

      <p><strong>Chef:</strong> {{ course.chef }}</p>

      <p><strong>Level:</strong> {{ course.level }}</p>

      <p><strong>Price:</strong> R{{ course.price }}</p>

      <p v-if="course.available" class="available">Available</p>

      <p v-else class="sold-out">SOLD OUT</p>

      <button @click="saveCourse(course.id)">
        {{ savedCourses.includes(course.id) ? "Saved" : "Save" }}
      </button>
    </div>
  </div>
</template>

<style>
body {
  background-color: #fff8f0;
  font-family: Arial, sans-serif;
}

h1 {
  text-align: center;
  color: #4a2c2a;
}

.wishlist {
  text-align: center;
  font-size: 18px;
  font-weight: bold;
}

.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 15px;
}

.card {
  width: 100%;
  max-width: 250px;
  padding: 15px;
  border-radius: 10px;
  background-color: white;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
}

.available {
  color: green;
  font-weight: bold;
}

.sold-out {
  color: red;
  font-weight: bold;
}

button {
  padding: 8px 12px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  background-color: #e67e22;
  color: white;
}

button:hover {
  opacity: 0.9;
}
</style>
