<template>
  <div class="result-container">
    <div class="row mt-2">
      <img :src="fetchedResult.Poster" :alt="fetchedResult.Title" class="img" />
    </div>
    <div class="info">
        <button @click="$router.go(-1)" class="backBtn">back</button>
        <h1 class="title">{{ fetchedResult.Title }}</h1>
        <span class="para">{{ fetchedResult.Type }}</span>
        <span class="para">{{ fetchedResult.Released }}</span>
        <p class="plot">Plot: <span class="para">{{fetchedResult.Plot}}</span></p>
        <p class="plot">Actors: <span class="para">{{fetchedResult.Actors}}</span></p>
        <p class="plot">Genre: {{fetchedResult.Genre}}</p>
        <p class="plot">IMDB Rating: {{fetchedResult.imdbRating}}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      id: this.$route.params.id,
      fetchedResult: [],
    };
  },
  created() {
    fetch("http://www.omdbapi.com/?apikey=92f8901f&i=" + this.id)
      .then((response) => response.json())
      .then((response) => {
        this.fetchedResult = response;
        console.log(response);
      });
  },
};
</script>

<style scoped>
.result-container{
    display: flex;
    flex-direction: row;
    gap: 32px;
    justify-content: center;
}

.img {
  width: 289px;
  height: 429px;
}

.title {
    font-style: normal;
    font-weight: 700;
    font-size: 40px;
    line-height: 52px;
    /* identical to box height */
    letter-spacing: -0.02em;
    color: #FFFFFF;
}

.para{
    font-style: normal;
    font-weight: 400;
    font-size: 16px;
    line-height: 21px;
    color: rgba(255, 255, 255, 0.55);
    text-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}

.plot{
    font-style: normal;
    font-weight: 400;
    font-size: 16px;
    line-height: 21px;
    color: #FFFFFF;
}

.info{
    width: 346px;
}

.backBtn{
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 21px;
  padding: 5px;
  border-color: var(--background-outline-btn-color);
  color: var(--background-outline-btn-color);
  background: none;
  border-radius: 10px;
}
</style>
