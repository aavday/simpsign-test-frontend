<script setup>
import UserCard from '../components/UserCard.vue'
import { ref } from 'vue'
import axios from 'axios'
import AddUserForm from '@/components/AddUserForm.vue'

const users = ref(null)

axios
  .get('http://localhost:8000/api/users/')
  .then(response => users.value = response.data)
</script>

<template>
  <main>
    <div class="container">
      <h2>Add user</h2>
      <AddUserForm />
      <h2>Users</h2>
      <div class="user-cards">
        <UserCard :user="user" :key="user.name" v-for="user in users" />
      </div>
    </div>
  </main>
</template>

<style>
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 15px;
}

.user-cards {
  padding-bottom: 50px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 15px;
}
</style>
