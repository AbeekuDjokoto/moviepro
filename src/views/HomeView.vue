<template>
  <div class="container">
    <div class="centery">
      <input
        type="text"
        class="input"
        placeholder="Enter movie title..."
        v-model="searchResult"
        @keyup.enter="searchTerm()"
      />
      <searchBtn :searchtxt="searchText" type="submit" @click="searchTerm" class="sub"></searchBtn>
    </div>
   
      <img src="../assets/Group15.svg" alt="" class="img" />
    
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
    };
  },
  methods: {
    async searchTerm() {
      await axios
        .get(`http://www.omdbapi.com/?apikey=92f8901f&s=${this.searchResult}`)
        .then((response) => {
          this.$router.push({path: "/searchResult"})
          console.log(response);
        });
    },
  },
};
</script>


<style scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.centery {
  display: flex;
  justify-content: center;
  position: relative;
}

.sub {
  position: absolute;
  top: 5px;
  right: 310px;
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
  cursor: pointer;
}

.input:focus {
  outline-color: var(--background-outline-btn-color);
}

.searchdiv {
  text-align: center;
}

.img {
  height: 278px;
  cursor: pointer;
  margin-top: 50px;
  z-index: 1;
}
</style>
