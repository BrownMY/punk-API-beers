<script>
import axios from 'axios';
import ListItem from './components/ListItem.vue';

export default {
  data() {
    return {
      url: 'https://api.punkapi.com/v2/beers?',
      pageLimit: 20,
      results: [],
      searchInput: ''
    }
  },
  mounted() {
    const response = axios.get(this.url + `per_page=${this.pageLimit}`).then(response => {
      this.results = response.data
    })
  },
  methods: {
    //WIP - Not working as of yet - needs to increase page limit by 20 on each click of the button
    // handlePageLimit() {
    //   let newPageLimit = this.pageLimit >= 60 ? 80 : this.pageLimit + 20
    //   this.pageLimit = newPageLimit
    // },

    // WIP - needs refactoring. A user can filter beers by typing the name, clicking out of the input filed, then clicking inside again. Currently needs reloading to fetch entire list again.
    handleSearchBar(input) {
      this.searchInput = input.target.value
      if (this.searchInput) {
        const response = axios.get(this.url + `beer_name=${input.target.value}`).then(response => {
          this.results = response.data
        })
      } else {
        const response = axios.get(this.url + `per_page=${this.pageLimit}`).then(response => {
          this.results = response.data
        })
      }
    }
  },
  components: {
    ListItem
  }
}
</script>

<template>
  <div class="app-container">
    <div class="header">
      <h3>Punk API Beers</h3>
      <input type="text" @click="handleSearchBar" v-model="input" placeholder="Type here to filter by name"
        class="search-bar">

    </div>
    <ListItem :results="this.results" />
    <button @click="handlePageLimit">load more beer</button>
  </div>

</template>

<style scoped>
.app-container {
  display: flex;
  flex-direction: column;
  width: 100vw;
  height: 100vh;
}

h3 {
  font-family: 'Montserrat', sans-serif;
  font-size: 24px;
  font-weight: 600px;
}

.header {
  display: flex;
  flex-direction: row;
  width: 95vw;
  margin-top: 2vh;
  justify-content: space-between;
  align-items: center;
}

.search-bar {
  width: 50vw;
  height: 20px;
  border: 2px solid rgb(227, 228, 230);
  border-radius: 3px;
  padding: 10px;
}

@media only screen and (max-width: 600px) {
  .header {
    display: flex;
    flex-direction: column;
    width: 85vw;
    margin-top: 2vh;
    justify-content: center;
    align-items: center;
  }

  .search-bar {
  width: 100vw;
  height: 20px;
  border: 2px solid rgb(227, 228, 230);
  border-radius: 3px;
  padding: 10px;
}
}
</style>
