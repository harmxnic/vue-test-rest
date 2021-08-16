<template>
  <li class="list__item">
    <span class="list__text">
          <span class="list__title">{{ title }}</span>
          <span class="list__descr">{{ body }}</span>
        </span>
    <button class="list__btn" @click="deleteCard">Delete</button>
  </li>
</template>

<script>
export default {
  name: "Card",
  props: ['title', 'body', 'card'],
  methods: {
    deleteCard() {
      this.$emit('remove', this.card)
    }
  }
}
</script>

<style scoped>

</style>