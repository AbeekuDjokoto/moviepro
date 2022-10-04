<template>
  <form class="search-container">
    <input type="text" class="input" placeholder="Enter movie title..." v-model="searchResult" @keyup.enter="searchTerm()"/>
    <searchButton :searchtxt="searchtxt" class="move" type="submit"></searchButton>
  </form>
</template>

<script>
import SearchButtonComponentVue from "./SearchButtonComponent.vue";
import axios from "axios"
export default {
  components: {
    searchButton: SearchButtonComponentVue,
  },
  data() {
    return {
      searchtxt: "Search",
      searchResult: ''
    };
  },
  methods: {
    async searchTerm(){
        await axios.get(`http://www.omdbapi.com/?apikey=92f8901f&s=${this.searchResult}`)
        .then((response) => {
            console.log(response)
        })
    }
  }
};
</script>

<style scoped>
.search-container{
    position: relative;
}

input{
    margin-bottom: 72px;
}

.input:focus {
  outline: none;
}

.input {
  background: #313030;
  border-radius: 92px;
  padding: 18px 0px;
  width: 507px;
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
  cursor: pointer;
}

.move {
  position: absolute;
  top: 5px;
  left: 390px;
}

@media screen and (max-width: 992px) {
  
}
</style>
