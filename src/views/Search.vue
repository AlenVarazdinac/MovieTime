<template>
  <div class="bg-black h-full">
    <div class="container mx-auto h-full bg-black">
      <!-- <h2 class="text-white text-center py-16 mx-auto">Search</h2> -->
      <!-- Movie Search Form -->
      <div class="mt-32 mb-16 lg:my-16 z-10 mx-auto">
        <form @submit="searchMovie" method="GET">
          <input
            type="search"
            class="bg-transparent border-b-2 border-grey-darkest pb-1 focus:border-green text-center w-64 text-xl mx-auto text-green outline-none"
            placeholder="Search ..."
            v-model="search"
          >
        </form>
      </div>
      <!-- Movie Search Form End -->
      <!--Search movies-->
      <div v-if="latestMovies.length > 0">
        <div
          class="container mx-auto my-4 flex flex-col lg:flex-row movies-total-width"
          v-for="i in Math.ceil(latestMovies.length / 5)"
          :key="i"
        >
          <div
            class="max-w-xs rounded shadow-none lg:mr-2 mb-4"
            v-for="movie in latestMovies.slice((i-1) * 5, i * 5)"
            :key="movie.id"
          >
            <router-link :to="movie.movie_link">
              <div class="relative movie_wrapper mx-auto w-full" v-if="latestMovies.length > 0">
                <img class="w-full movie_poster" :src="movie.poster_path" :alt="movie.title">
                <p
                  class="card-text text-base text-white absolute pin-t pin-r mx-auto text-center w-full p-2"
                >{{ movie.overview }}</p>
                <p
                  class="card-rating text-green text-lg absolute pin-b pin-r mx-auto text-center w-full p-2 pb-4"
                >
                  <i class="fas fa-star"></i>
                  {{ movie.rating / 2}}
                </p>
              </div>
            </router-link>
          </div>
        </div>
      </div>
      <div class="relative mx-auto w-full" v-else-if="this.$route.path == '/search'">
        <p class="text-white text-lg"></p>
      </div>
      <div class="relative mx-auto w-full" v-else-if="latestMovies.length <= 0">
        <p class="text-white text-lg">There are no movies that match your search.</p>
      </div>
      <!--Search movies end-->
    </div>
  </div>
</template>

<style lang="scss" scoped>
.movie_poster {
  min-height: 26rem;
  max-height: 26rem;
}
</style>


<script>
import axios from "axios";

export default {
  name: "search",
  created() {
    this.listMovie();
  },
  data() {
    return {
      search: "",
      movies: [],
      latestMovies: [],
      currentMovie: []
    };
  },
  methods: {
    searchMovie(e) {
      this.$router.push("/search/" + this.search);
    },
    listMovie() {
      axios
        .get(
          "https://api.themoviedb.org/3/search/movie?api_key=625d11b03471b152a801f7f8bf8f34ac&language=en-US&query=" +
            this.$route.params.title +
            "&page=1&include_adult=false"
        )
        .then(response => {
          var i;
          this.movies = response.data.results;
          this.movies = this.movies.slice(0, 5);
          // console.log(this.movies);
          for (i in this.movies) {
            if (this.movies[i].poster_path != null) {
              this.currentMovie = {
                id: this.movies[i].id,
                title: this.movies[i].original_title,
                rating: this.movies[i].vote_average,
                poster_path:
                  "https://image.tmdb.org/t/p/w500" +
                  this.movies[i].poster_path,
                overview: this.movies[i].overview.substring(0, 250) + "...",
                movie_link: "/movies/" + this.movies[i].id
              };
              this.latestMovies.push(this.currentMovie);
            }
          }
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
