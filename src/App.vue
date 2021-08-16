<template>
  <div class="container">
    <div class="flex">
      <Form
          @create="pushCard"
      />
      <Filter
        v-model="selectedOption"
        :sortOptions="sortOptions"
      />
    </div>
    <div class="app-nav">
      <input
          class="app-input"
          type="text"
          placeholder="Search by title"
          v-model="searchQuery"
      >
      <div class="app-pages">
        <div
            v-for="pageNum in pagesCount"
            :key="pageNum"
            class="app-page"
            :class="{
              'app-page_current': pageNum === page
            }"
            @click="setCurrentPage(pageNum)"
        >
          {{pageNum}}</div>
      </div>
    </div>
    <CardList
        v-if="!isLoading"
        :cards="sortedByQuery"
        @remove="deleteCard"
    />
    <div class="app-loader" v-else>Cards are loading...</div>
  </div>
</template>

<script>
import Form from "@/components/Form";
import CardList from "@/components/CardList";
import axios from "axios";
import Filter from "@/components/Filter";

export default {
  components: {
    Filter,
    Form,
    CardList
  },
  data() {
    return {
      cards: [],
      selectedOption: '',
      page: 1,
      limit: 5,
      pagesCount: 0,
      sortOptions: [
        {value: 'title', name: 'Sort by title'},
        {value: 'body', name: 'Sort by description'}
      ],
      searchQuery: '',
      isLoading: true
    }
  },
  methods: {
    async fetchData() {
      const fetchCards = await axios.get('https://jsonplaceholder.typicode.com/posts', {
        params: {
          _page: this.page,
          _limit: this.limit
        }
      })
      this.pagesCount = Math.ceil(fetchCards.headers['x-total-count'] / this.limit)
      this.cards = fetchCards.data
      this.isLoading = false
    },
    pushCard(card) {
      this.cards = [card, ...this.cards]
    },
    deleteCard(card) {
      this.cards = this.cards.filter(el => card.id !== el.id)
    },
    setCurrentPage(pageNum) {
      this.page = pageNum
    }

  },
  computed: {
    sortedCards() {
      return [...this.cards].sort((a, b) => {
        return a[this.selectedOption]?.localeCompare(b[this.selectedOption])
      })
    },
    sortedByQuery() {
      return this.sortedCards.filter(card => card.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    }
  },
  watch: {
    // selectedOption() {
    //   this.cards.sort((a, b) => {
    //     return a[this.selectedOption]?.localeCompare(b[this.selectedOption])
    //   })
    // }
    page() {
      this.fetchData()
    }
  },
  mounted() {
    this.fetchData()
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  font-family: "Tahoma", sans-serif;
}

.container {
  max-width: 1440px;
  margin: 0 auto;
}

.flex {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.app-nav {
  display: flex;
  justify-content: space-between;
  margin-bottom: 3rem;
}

.app-pages {
  display: flex;
  justify-content: space-between;
  align-self: center;
  gap: 10px;
}

.app-page {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 5px;
  width: 20px;
  height: 20px;
  border: 1px solid lightgray;
  transition: all .5s ease;
  cursor: pointer;
  &:hover {
    background: blue;
    color: white;
  }
  &_current {
    background: darkblue;
    color: white;
    pointer-events: none;
  }
}

.app-input {
  align-self: center;
  padding: 1.2rem;
  width: 300px;
  box-sizing: border-box;
  font-size: 1.5rem;
}

.app-loader {
  font-size: 2rem;
  font-weight: 600;
}
</style>
