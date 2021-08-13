<template>
  <div class="container">
    <Form
        @create="pushCard"
    />
    <CardList
        :cardList="cards"
    />
  </div>
</template>

<script>
import Form from "@/components/Form";
import CardList from "@/components/CardList";

export default {
  components: {
    Form,
    CardList
  },
  data() {
    return {
      cards: []
    }
  },
  methods: {
    pushCard(card) {
      this.cards.push(card)
    },
    deleteCard(card) {

    }
  },
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
}

.container {
  max-width: 1440px;
  margin: 0 auto;
}

.form {
  border: 1px solid darkgoldenrod;
  width: 50%;
  margin: 5rem auto;
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
