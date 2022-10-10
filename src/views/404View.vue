<template>
  <div class="text-center">
    <h1 class="text-danger mb-5">Page not found</h1>
    <router-link to="/"><button class="btn btn-outline-danger">Home</button></router-link>
  </div>
</template>

<script>

export default {
  
  data() {
    return {
      searchText: "Search",
      searchResult: "",
      searchedItems: [],
      searchNotFound: false,
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

.dotty{
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

.img{
  width: 200px;
  height: 295.4px;
  cursor: pointer;
}
</style>
