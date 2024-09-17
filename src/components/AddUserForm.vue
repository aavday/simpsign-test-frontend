<script setup>
import { ref } from 'vue'
import axios from 'axios'

const name = ref(null);
const email = ref(null);
const description = ref(null);
const errors = ref(null);
const success = ref(false);

const submit = async () => {
  const data = {
    email: email.value,
    name: name.value,
    description: description.value
  }
  axios
    .post('http://localhost:8000/api/users/create/', data)
    .then(() => errors.value = null)
    .catch(error => {
      console.log(error.response)
      errors.value = error.response.data.errors
    })
    .then(() => success.value = !errors.value)
}
</script>

<template>
  <form action="" @submit.prevent="submit" class="add-user-form" v-if="!success">
    <div class="form-group">
      <label for="name">Name</label>
      <input type="text" class="form-input" id="name" name="name" v-model="name" required>
      <template v-if="errors && errors.name">
        <div class="form-input__error" v-for="error in errors.name" :key="error" >
          {{ error }}
        </div>
      </template>
    </div>
    <div class="form-group">
      <label for="email">Email</label>
      <input type="email" class="form-input" id="email" name="email" v-model="email" required>
      <template v-if="errors && errors.email">
        <div class="form-input__error" v-for="error in errors.email" :key="error" >
          {{ error }}
        </div>
      </template>
    </div>
    <div class="form-group">
      <label for="description">Description (навыки через запятую)</label>
      <input type="text" class="form-input" id="description" name="description" v-model="description" required>
      <template v-if="errors && errors.description">
        <div class="form-input__error" v-for="error in errors.description" :key="error" >
          {{ error }}
        </div>
      </template>
    </div>
    <div class="form-group">
      <button type="submit">Submit</button>
    </div>
  </form>
  <div v-else class="form-success">
    New user is successfully added
  </div>
</template>

<style scoped lang="scss">
.form {
  max-width: 600px;

  &-input {
    display: block;

    &__error {
      color: red;
      margin: 5px 0;
      font-size: 0.8em;
    }
  }

  &-group {
    padding: 10px 0;
  }

  &-success {
    color: green;
  }
}
</style>
