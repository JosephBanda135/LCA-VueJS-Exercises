<script setup>
defineProps({
  name: String,
  coach: String,
  date: String,
  time: String,
  capacity: Number,
});
</script>

<template>
  <div class="card">
    <h2>{{ name }}</h2>
    <p>Coach: {{ coach }}</p>
    <p>Date: {{ date }}</p>
    <p>Time: {{ time }}</p>
    <p>Capacity: {{ capacity }}</p>

    <button @click="$emit('delete-session')">Delete</button>
  </div>
</template>

<style>
.card {
  width: 250px;
  padding: 15px;
  border-radius: 10px;
  border-left: 5px solid #42b983;
  background: #ffffff;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.card:hover {
  transform: translateY(-5px);
}

h2 {
  color: #42b983;
}

button {
  margin-top: 10px;
  padding: 8px 12px;
  cursor: pointer;
  background-color: #ff6b6b;
  color: white;
  border: none;
  border-radius: 5px;
}

button:hover {
  background-color: #e74c3c;
}
</style>
