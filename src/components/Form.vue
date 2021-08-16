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
        :style="!(post.title && post.body)
        ? 'opacity: 0.5; pointer-events: none;'
        : 'opacity: 1; pointer-events: unset;'"
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
        id: Date.now()
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.form {
  border: 1px solid darkgoldenrod;
  width: 50%;
  margin: 5rem 0;
  display: flex;
  justify-content: space-between;
  padding: 40px;
  border-radius: 10px;
  &__inputs {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }
  &__title, &__body {
    padding: 10px;
    box-sizing: border-box;
    border-radius: 5px;
    border: 1px solid lightgray;
  }
  &__btn {
    align-self: center;
    padding: 10px;
    color: darkgoldenrod;
    background: transparent;
    border: 1px solid lightgray;
    border-radius: 10px;
    font-size: 1rem;
    cursor: pointer;
    transition: all .3s ease;
    &:hover {
      color: white;
      background: firebrick;
      border-color: lightgray;
    }
  }
}
</style>