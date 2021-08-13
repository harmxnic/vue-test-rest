<template>
  <ul class="list">
    <Card
        v-if="cards.length"
        v-for="card in cards.concat(cardList)"
        :key="card.id"
        :id="card.id"
        :title="card.title"
        :body="card.body"
        :card="card"
        :deleteCard="deleteCard"
    />
    <li class="list__null" v-else>No items in list</li>
  </ul>
</template>

<script>
import Card from "@/components/Card";

export default {
  components: {
    Card
  },
  //TODO - совместить cardList и cards
  //TODO - сделать сортировку
  //TODO - вернуть delete
  props: ['cardList'],
  data() {
    return {
      cards: []
    }
  },
  name: "CardList",
  methods: {
    fetchData() {
      fetch('https://jsonplaceholder.typicode.com/posts/1')
          .then(res => res.json())
          .then(res => this.cards.push(res))
          .catch(e => console.log(e))
    },
    deleteCard() {
      //this.cards = this.cards.filter(el => el.id !== card.id)
    }
  },
  mounted() {
    this.fetchData()
  }
}
</script>

<style lang="scss">
.list {
  display: flex;
  flex-direction: column;
  gap: 40px;
  list-style-type: none;
  font-family: 'Tahoma', sans-serif;

  &__item {
    width: 100%;
    padding: 20px;
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
</style>