<template>
  <div>
    <div class="container">
      <div class="input-container">
        <input
        type="text"
        class="input"
        placeholder="Enter movie title..."
        v-model="searchResult"
        @keyup.enter="searchTerm()"
      />
      <searchBtn :searchtxt="searchText" type="submit" @click="searchTerm" class="sub"></searchBtn>
      </div>
      
    </div>

    <div class="card">
      <div v-for="item in searchedItems" :key="item.imdbID">
        <router-link :to="'/singleView/' + item.imdbID"
            ><img :src="item.Poster" alt="" class="img"/></router-link>
        <h1 class="title">{{ item.Title }}</h1>
        <span class="type">{{ item.Type }}</span>
        <span class="dot">.</span> <span class="year">{{ item.Year }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import SearchInputComponentVue from "@/components/SearchInputComponent.vue";
import SearchButtonComponentVue from "@/components/SearchButtonComponent.vue";
import axios from "axios";
export default {
  components: {
    searchInputField: SearchInputComponentVue,
    "searchBtn": SearchButtonComponentVue
  },
  data() {
    return {
      searchText: "Search",
      searchResult: "",
      searchedItems: [],
      searchNotFound: "",
    };
  },
  methods: {
    async searchTerm() {
      await axios
        .get(`http://www.omdbapi.com/?apikey=92f8901f&s=${this.searchResult}`)
        .then((response) => {
          this.searchedItems = response.data.Search;
          console.log(this.searchedItems);
          if (response.data.Search == null) {
            this.searchNotFound = "Search result not found";
          }
        })
        .catch((err) => console.log(err));
    },
  },
};
</script>

<style scoped>
.container {
  text-align: center;
}

.input-container{
  display: relative;
}

.input {
  background: #313030;
  border-radius: 92px;
  padding: 18px 0px;
  max-width: 507px;
  width: 70%;
}

.input[type="text"] {
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 21px;
  color: rgba(255, 255, 255, 0.5);
  border: none;
  cursor: pointer;
  padding-left: 10px;
}

.input:focus{
  outline-color: var(--background-outline-btn-color);
}

.sub {
  position: absolute;
  margin-top: 5px;
  margin-left: -115px;
}

.title {
  font-style: normal;
  font-weight: 700;
  font-size: 16px;
  line-height: 21px;
  color: #ffffff;
  max-width: 200px;
}

.type {
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 21px;
  color: rgba(255, 255, 255, 0.55);
  text-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}

.year {
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 21px;
  color: rgba(255, 255, 255, 0.55);
  text-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}

.dot {
  background: rgba(255, 255, 255, 0.55);
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}

.card {
  display: flex;
  flex-direction: row;
  gap: 30px 10px;
  flex-wrap: wrap;
  justify-content: space-evenly;
  background: none;
  border: none;
  margin-top: 72px;
}

.img{
  width: 200px;
  height: 295.4px;
  cursor: pointer;
}
</style>
