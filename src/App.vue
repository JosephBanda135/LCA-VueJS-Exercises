<script setup>
import { ref, computed } from "vue";
import FitnessClass from "./components/FitnessClass.vue";

const sessions = ref([
  {
    id: 1,
    name: "Yoga",
    coach: "Sarah",
    date: "2026-06-15",
    time: "09:00",
    capacity: 20,
  },
  {
    id: 2,
    name: "Pilates",
    coach: "John",
    date: "2026-06-16",
    time: "10:30",
    capacity: 15,
  },
  {
    id: 3,
    name: "Spinning",
    coach: "Lisa",
    date: "2026-06-17",
    time: "18:00",
    capacity: 25,
  },
]);

const totalSessions = computed(() => {
  return sessions.value.length;
});

const className = ref("");
const coachName = ref("");
const classDate = ref("");
const classTime = ref("");
const classCapacity = ref("");

function addSession() {
  if (
    !className.value ||
    !coachName.value ||
    !classDate.value ||
    !classTime.value ||
    !classCapacity.value
  ) {
    alert("Please fill in all fields");
    return;
  }

  sessions.value.push({
    id: Date.now(),
    name: className.value,
    coach: coachName.value,
    date: classDate.value,
    time: classTime.value,
    capacity: Number(classCapacity.value),
  });

  className.value = "";
  coachName.value = "";
  classDate.value = "";
  classTime.value = "";
  classCapacity.value = "";
}

function deleteSession(id) {
  sessions.value = sessions.value.filter((session) => session.id !== id);
}
</script>

<template>
  <h1>FlexZone Fitness</h1>
  <p>Manage your fitness class schedule.</p>
  <p>Total Sessions: {{ totalSessions }}</p>
  <div class="form">
    <input v-model="className" placeholder="Class Name" />

    <input v-model="coachName" placeholder="Coach Name" />

    <input v-model="classDate" type="date" />

    <input v-model="classTime" type="time" />

    <input v-model="classCapacity" type="number" placeholder="Capacity" />

    <button @click="addSession">Add Session</button>
  </div>
  <div v-if="sessions.length === 0">
    <p class="empty-message">No sessions scheduled</p>
  </div>

  <div v-else class="container">
    <FitnessClass
      v-for="session in sessions"
      :key="session.id"
      :name="session.name"
      :coach="session.coach"
      :date="session.date"
      :time="session.time"
      :capacity="session.capacity"
      @delete-session="deleteSession(session.id)"
    />
  </div>
</template>

<style>
body {
  font-family: Arial, sans-serif;
}

.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 20px;
  gap: 20px;
  margin-top: 20px;
}
.form {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 10px;
  margin: 20px;
}

.form input {
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

.form button {
  padding: 8px 15px;
  cursor: pointer;
}
p {
  text-align: center;
}
.empty-message {
  text-align: center;
  font-size: 18px;
  margin-top: 20px;
}

h1 {
  text-align: center;
  color: #2c3e50;
}

.form button {
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 5px;
}

.form button:hover {
  opacity: 0.9;
}
</style>
