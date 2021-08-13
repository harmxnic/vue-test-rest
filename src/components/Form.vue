<template>
  <form class="form" @submit.prevent>
    <div class="form__inputs">
      <input
          type="text"
          class="form__title"
          v-model="post.title"
          placeholder="Card Title"
      >
      <input
          type="text"
          class="form__body"
          v-model="post.body"
          placeholder="Card Body"
      >
    </div>
    <button
        class="form__btn"
        @click="pushCard"
        :disabled="!(post.title && post.body)"
    >
      Add card
    </button>
  </form>
</template>

<script>
export default {
  name: "Form",
  data() {
    return {
      post: {
        title: '',
        body: '',
        id: Date.now()
      }
    }
  },
  methods: {
    pushCard() {
      this.$emit('create', this.post)
      this.post = {
        title: '',
        body: '',
      }
    }
  }
}
</script>

<style scoped>

</style>