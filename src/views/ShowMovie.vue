<template>
  <!--Show movie -->
  <div class="container-fluid bg-black h-screen">
    <div class="container mx-auto">
      <div
        class="flex flex-col lg:flex-row pt-16 lg:pt-0 items-center h-screen"
        v-if="currentMovie.status != null"
      >
        <div class="w-full p-8 lg:p-0 lg:w-1/3 self-center">
          <img :src="currentMovie.poster_path" :alt="currentMovie.title" class="shadow-lg w-full">
        </div>
        <div class="w-full p-8 lg:p-0 lg:w-2/3 text-left lg:ml-8 self-center">
          <h1 class="text-green text-5xl mb-4">{{ currentMovie.title }}</h1>
          <p class="text-grey-light text-lg mb-4 whitespace-pre-wrap">{{ currentMovie.overview }}</p>
          <div class="flex">
            <button
              class="bg-green hover:bg-green-dark text-white font-bold py-3 px-6 rounded mr-4"
            >
              Watch Now
              <i class="fas fa-play pl-2"></i>
            </button>
            <p class="text-green text-2xl text-left self-center">
              <i class="fas fa-star"></i>
              {{ currentMovie.rating / 2}}
            </p>
          </div>
        </div>
      </div>
      <div class="flex items-center h-screen mx-auto" v-else>
        <p class="text-white text-lg text-center w-full">There are no movies that match your search.</p>
      </div>
    </div>
  </div>
  <!--Show movie end-->
</template>

<style lang="scss">
</style>


<script>
import axios from "axios";

export default {
  name: "showMovie",
  created() {
    this.listMovie();
  },
  data() {
    return {
      movies: [],
      latestMovies: [],
      currentMovie: []
    };
  },
  methods: {
    listMovie() {
      axios
        .get(
          "https://api.themoviedb.org/3/movie/" +
            this.$route.params.movieId +
            "?api_key=625d11b03471b152a801f7f8bf8f34ac&language=en-US"
        )
        .then(response => {
          console.log(response);
          var i;
          this.movies = response.data;
          console.log(this.movies);
          this.currentMovie = {
            id: this.movies.id,
            title: this.movies.original_title,
            rating: this.movies.vote_average,
            poster_path:
              "https://image.tmdb.org/t/p/w500" + this.movies.poster_path,
            overview: this.movies.overview,
            movie_link: "/movies/" + this.movies.id,
            status: response.data.status
          };
          this.latestMovies.push(this.currentMovie);
          console.log(this.currentMovie);
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>

<style lang="scss" scoped>
.movies-total-width {
  width: 20rem;
}
.movie_wrapper {
  transition: 0.2s;
  position: center;
  &:hover {
    cursor: pointer;
    .movie_poster {
      opacity: 0.2;
      filter: blur(2px);
      -webkit-filter: blur(2px);
    }
    .card-text {
      visibility: visible;
    }
    .card-rating {
      visibility: visible;
    }
  }
}
.movie_poster {
  width: auto;
  height: auto;
  transition: 0.2s;
}
.card-text {
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  visibility: hidden;
}

.card-rating {
  visibility: hidden;
}

@media (min-width: 992px) {
  .movies-total-width {
    width: 100rem;
  }
}
</style>
