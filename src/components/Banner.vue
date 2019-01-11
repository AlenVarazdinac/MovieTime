<template>
  <div class="container-fluid">
    <img
      src="../assets/banner.jpg"
      class="banner-image bg-contain bg-no-repeat bg-top bg-fixed opacity-75 lg:opacity-100 z-0"
    >

    <!-- Search bar -->
    <div class="absolute pin-t pin-r mr-8 my-10 invisible z-10 md:visible">
      <form @submit.stop.prevent="searchMovie" method="GET">
        <input
          type="search"
          class="bg-black shadow rounded-full border-0 p-3 pl-10 text-green outline-none"
          placeholder="Search ..."
          v-model="search"
        >
        <div class="absolute pin-l pin-t mt-3 ml-4 text-purple-lighter">
          <i class="fas fa-search text-green"></i>
        </div>
      </form>
    </div>
    <!-- Search bar end -->
    <!-- Banner text -->
    <div class="banner-text text-center lg:text-left z-10 mx-auto w-full lg:w-1/4">
      <h2 class="text-green text-3xl lg:text-5xl">Venom</h2>
      <p class="text-white text-sm md:text-lg lg:text-xl whitespace-pre-line mb-5">
        When Eddie Brock acquires the powers of
        a symbiote, he will have to release his alter-ego
        "Venom" to save his life.
      </p>
      <star-rating
        v-bind:increment="0.5"
        inactive-color="#22292F"
        active-color="#38c172"
        v-bind:star-size="35"
        :read-only="true"
        :rating="3.4"
        :round-start-rating="false"
        border-color="#38c172"
        :border-width="2"
        text-class="custom-rating-text"
      ></star-rating>
      <router-link to="/movies/335983">
        <button class="bg-green hover:bg-green-dark text-white font-bold py-3 px-6 rounded mt-8">
          Watch Now
          <i class="fas fa-play pl-2"></i>
        </button>
      </router-link>
    </div>
    <!-- Banner text end -->
  </div>
</template>

<style lang="scss">
div.vue-star-rating {
  margin-left: auto;
  margin-right: auto;
}
.banner-image {
  height: 100%;
  width: 100%;
}
.custom-rating-text {
  color: #38c172;
  font-size: 1.25rem;
}
.banner-text {
  position: relative;
  top: 0%;
  left: 0%;
  transform: translate(0%, 0%);
}
@media (min-width: 768px) {
  .banner-text {
    position: absolute;
    top: 10%;
    left: 0%;
    transform: translate(0%, 0%);
  }
}
@media (min-width: 992px) {
  .banner-text {
    position: absolute;
    top: 45%;
    left: 30%;
    transform: translate(-50%, -50%);
  }
  div.vue-star-rating {
    margin-left: 0;
    margin-right: 0;
  }
}
</style>

<script>
// @ is an alias to /src
import MovieCard from "@/components/MovieCard.vue";
import StarRating from "vue-star-rating";

export default {
  name: "home",
  components: {
    MovieCard,
    StarRating
  },
  data() {
    return {
      search: ""
    };
  },
  methods: {
    searchMovie(e) {
      e.preventDefault();
      this.$router.push("/search/" + this.search);
    }
  }
};
</script>