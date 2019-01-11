<template>
  <div class="container mx-auto mt-20">
    <h2 class="text-white text-left pl-4 lg:pl-0">Popular Movies</h2>
    <!--Popular movies-->
    <div class="container mx-auto my-8 flex flex-col lg:flex-row movies-total-width">
      <div
        class="max-w-xs rounded shadow-none m-0 lg:mr-2 mb-4"
        v-for="movie in popularMovies"
        :key="movie.id"
      >
        <router-link :to="movie.movie_link">
          <div class="relative movie_wrapper mx-auto w-full">
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
    <!--Popular movies end-->
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "PopularMovies",
  data: function() {
    return {
      title: "",
      released: "",
      rating: "",
      poster_path: "",
      movies: [],
      popularMovies: [],
      currentMovie: []
    };
  },
  props: {
    msg: String
  },
  methods: {
    getMovies() {
      axios
        .get(
          "https://api.themoviedb.org/3/movie/popular?api_key=625d11b03471b152a801f7f8bf8f34ac&language=en-US&page=1"
        )
        .then(response => {
          var i;
          this.movies = response.data.results;
          this.movies = this.movies.slice(0, 4);
          for (i in this.movies) {
            this.currentMovie = {
              id: this.movies[i].id,
              title: this.movies[i].original_title,
              rating: this.movies[i].vote_average,
              poster_path:
                "https://image.tmdb.org/t/p/w500" + this.movies[i].poster_path,
              overview: this.movies[i].overview,
              movie_link: "/movies/" + this.movies[i].id
            };
            this.popularMovies.push(this.currentMovie);
          }
        })
        .catch(error => {
          console.log(error);
        });
    }
  },
  created() {
    this.getMovies();
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
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
