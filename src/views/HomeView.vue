<template>
  <div class="container">
    <div class="centery">
      <input
        type="text"
        class="input text-align-center"
        placeholder="Enter movie title..."
        v-model="searchResult"
        @keyup.enter="searchTerm()"
      />
      <searchBtn
        :searchtxt="searchText"
        type="submit"
        @click="searchTerm"
        class="sub"
      ></searchBtn>
    </div>

    <h1 class="text-danger text-center mt-2" v-if="isShown">
      Movie not found! Try another.
    </h1>

    <img
      :src="landingImg"
      alt=""
      class="img img-fluid"
      v-if="(searchedItems.length == 0) & (spinner == false)"
    />

    <div class="card" v-else>
      <div v-for="item in searchedItems" :key="item.imdbID" class="hov-effect">
        <router-link :to="'/singleView/' + item.imdbID"
          ><img :src="item.Poster" alt="" class="img-card"
        /></router-link>
        <h1 class="title">{{ item.Title }}</h1>
        <span class="type"
          >{{ item.Type }}
          <img src="../assets/dot.svg" alt="dot" class="dotty" />
          {{ item.Year }}</span
        >
      </div>
    </div>

    <div class="row justify-content-center" v-if="spinner">
      <div
        class="spinner-border text-primary"
        style="width: 6rem; height: 6rem"
        role="status"
      >
        <span class="visually-hidden">Loading...</span>
      </div>
    </div>

    <div class="pagination-flex mt-5">
      <div v-for="page in Math.ceil(this.totalResults / 10)" :key="page">
        <div>
          <button
            @click="selectedNumber(page)"
            class="btn btn-outline-secondary active"
            type="button"
            :class="['page', { isActive: page === pageNumber }]"
          >
            {{ page }}
          </button>
        </div>
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
    searchBtn: SearchButtonComponentVue,
  },
  data() {
    return {
      searchText: "Search",
      searchResult: "",
      searchedItems: [],
      myTotalResultsArr: [],
      searchNotFound: "this",
      isShown: false,
      totalResults: null,
      pageNumber: 1,
      pageNull: null,
      landingImg: require("../assets/Group15.png"),
      spinner: false,
    };
  },
  computed: {
    totalResultsCalc() {
      return Math.ceil(this.totalResults / 10);
    },
  },
  created() {
    this.spinner = true;
  },
  beforeMount() {
    this.spinner = false;
  },
  watch: {
    pageNumber() {
      const { pageNumber } = this;
      this.searchTerm(pageNumber);
    },
  },
  methods: {
    async searchTerm(pageNumber) {
      this.spinner = true;
      await axios
        .get(
          `https://www.omdbapi.com/?apikey=92f8901f&s=${this.searchResult}&page=${pageNumber}`
        )
        .then((response) => {
          this.totalResults = Number(response.data.totalResults);
          if (response.data.Error) {
            this.isShown = true;
            this.searchedItems = [];
            this.landingImg = "";
            console.log("result:" + " " + response.data.Error);
            return;
          }
          this.searchedItems = response.data.Search;
          this.isShown = false;
          this.spinner = false;
        })
        .catch((err) => console.log("there was an error" + err));
    },
    selectedNumber(e) {
      this.pageNumber = e;
      console.log(this.pageNumber);
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
  background: #313030;
  border-radius: 92px;
  width: auto;
  min-width: 70%;
  padding: 6px 0;
  margin: 0 auto;
  position: sticky;
  top: 90px;
  z-index: 2;
}

.centery:focus-within {
  border: 2px solid var(--background-outline-btn-color);
}

.input {
  background: #313030;
  border: none;
  padding: 18px 0px;
  margin-left: 24px;
  width: 100%;
  outline: none;
}

.input[type="text"] {
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 21px;
  color: rgba(255, 255, 255, 0.5);
  padding-left: 10px;
  cursor: pointer;
}

input:focus {
  border: none;
  outline-color: none;
}

.sub {
  margin-right: 5px;
}

.img {
  height: 278px;
  cursor: pointer;
  margin-top: 50px;
  z-index: 1;
  object-fit: contain;
}

.img:hover,
.hov-effect:hover {
  transform: scale(1.1);
  transition: 0.3s;
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

.dotty {
  margin-top: 5px;
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

.foo-hover:hover {
  transform: scale(1.3);
}

.img-card {
  width: 200px;
  height: 295.4px;
  cursor: pointer;
}

.pagination-flex {
  display: flex;
  flex-wrap: nowrap;
  gap: 5px;
  z-index: 1;
  overflow-x: auto;
  justify-content: flex-start;
}

.isActive {
  background: var(--background-outline-btn-color);
}

.active:hover {
  background: white;
}
</style>
