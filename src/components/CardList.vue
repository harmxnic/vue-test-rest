<template>
  <transition-group
      tag="ul"
      name="card-list"
      class="list"
      v-if="cards.length"
  >
    <Card
        v-for="card in cards"
        :key="card.id"
        :id="card.id"
        :title="card.title"
        :body="card.body"
        :card="card"
        @remove="deleteCard"
    />
  </transition-group>
  <div class="list__null" v-else>No items in list</div>
</template>

<script>
import Card from "@/components/Card";

export default {
  components: {
    Card
  },
  props: ['cards'],
  data() {
    return {

    }
  },
  name: "CardList",
  methods: {
    deleteCard(card) {
      this.$emit('remove', card)
    }
  }
}
</script>

<style lang="scss">
.list {
  display: flex;
  flex-direction: column;
  gap: 40px;
  list-style-type: none;

  &__item {
    width: 100%;
    padding: 20px;
    box-sizing: border-box;
    border: 1px solid darkblue;
    border-radius: 10px;
    display: flex;
    justify-content: space-between;
  }

  &__null {
    font-size: 2rem;
    font-weight: 700;
    text-align: center;
  }

  &__text {
    display: flex;
    flex-direction: column;
    gap: 15px;
    width: 65%;
  }

  &__title {
    font-weight: 600;
    font-size: 1.5rem;
    line-height: 40px;
  }

  &__descr {
    font-size: 1.2rem;
    line-height: 26px;
  }

  &__btn {
    align-self: center;
    padding: 10px;
    color: firebrick;
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

.card-list-item {
  display: inline-block;
  margin-right: 10px;

}

.card-list-leave-active,
.card-list-enter-to-active {
  transition: all .5s ease;
  transform: translateX(30px);
}

.card-list-enter-to,
.card-list-leave-from {
  opacity: 1;
  transition: all .5s ease;
  transform: translateX(0);
}

.card-list-enter-from,
.card-list-leave-to {
  opacity: 0;
  transition: all .5s ease;
  transform: translateX(30px);
}
</style>