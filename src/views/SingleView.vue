<template>
  <div class="container">
    <div class="row mt-2 justify-content-center">
      <img
        :src="fetchedResult.Poster"
        :alt="fetchedResult.Title"
        class="img img-fluid"
      />
    </div>
    <div class="info mt-3">
      <button @click="$router.go(-1)" class="backBtn">
        <img src="../assets/arrow.svg" alt="back arrow" /> back
      </button>
      <h1 class="title">{{ fetchedResult.Title }}</h1>
      <span class="para align"
        >{{ fetchedResult.Type }}
        <img src="../assets/dot.svg" alt="dot" class="dot" />
        {{ fetchedResult.Released }}</span
      >
      <p class="plot mt-2 fetched-plot">
        Plot: <span class="para">{{ fetchedResult.Plot }}</span>
      </p>
      <p class="plot">
        Actors: <span class="para">{{ fetchedResult.Actors }}</span>
      </p>

      <p class="plot">
        Genre:
        <span v-for="genre in fetchedResult.Genre.split(',')" :key="genre">
          <button class="genreBtn mb-2">{{ genre }}</button>
        </span>
      </p>
      <p class="plot">
        IMDB Rating: {{ fetchedResult.imdbRating }}
        <img
          src="../assets/starremovebg.png"
          alt="star-icon"
          class="star-img"
        />
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      id: this.$route.params.id,
      fetchedResult: [],
      rating: [],
    };
  },
  created() {
    fetch("http://www.omdbapi.com/?apikey=92f8901f&i=" + this.id)
      .then((response) => response.json())
      .then((response) => {
        this.fetchedResult = response;
        this.rating = response.Genre.split(",");
      });
  },
};
</script>

<style scoped>
.result-container {
  display: flex;
  flex-direction: row;
  gap: 32px;
  justify-content: center;
}

.img {
  z-index: 1;
}

.title {
  font-style: normal;
  font-weight: 700;
  font-size: 40px;
  line-height: 52px;
  letter-spacing: -0.02em;
  color: #ffffff;
}

.para {
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 21px;
  color: rgba(255, 255, 255, 0.55);
  text-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}

.align {
  align-items: center;
}

.plot {
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 21px;
  color: #ffffff;
}

.backBtn {
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 21px;
  border-color: var(--background-outline-btn-color);
  color: var(--background-outline-btn-color);
  background: none;
  padding: 5.5px 24px;
  border-radius: 20px;
}

.dot {
  margin-top: 5px;
}

.star-img {
  height: 18px;
  position: relative;
  margin-top: -5px;
}

.genreBtn {
  background: #373636;
  border-radius: 50px;
  border: none;
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  line-height: 16px;
  color: rgba(255, 255, 255, 0.4);
  padding: 8px 24px;
  margin-right: 8px;
}

@media (min-width: 326px) {
  .container {
    vertical-align: middle;
  }

  .img{
    /* max-width: 400px; */
    width: 100%;
  }
}

@media (min-width: 760px){
  .container{
    display: flex;
    flex-direction: row;
    gap: 32px;
    justify-content: center;
  }

  .info{
    width: 500px;
    max-width: calc(100vw - 20px);
  }
}


</style>
