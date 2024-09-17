<script setup>
defineProps(['user'])
</script>

<template>
  <div class="user-card">
    <div class="user-card__name">{{ user.name }}</div>
    <div class="user-card__email">{{ user.email }}</div>
    <div class="user-card__description" v-if="user.description">
      Description:
      <template v-for="(skill, index) in user.description">
        {{ index === 0 ? skill : ', ' + skill }}
      </template>
    </div>
  </div>
</template>

<style scoped lang="scss">
.user-card {
  box-shadow: 4px 4px 8px 0 rgba(34, 60, 80, 0.2);
  padding: 15px;
  border-radius: 10px;

  &__name {
    font-weight: bold;
  }

  &__description {
    margin-top: 15px;
  }
}
</style>
