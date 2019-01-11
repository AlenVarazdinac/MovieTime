<template>
  <div class="container mx-auto mt-20">
    <h2 class="text-white text-left">Popular Movies</h2>
    <MovieCard/>
  </div>
</template>

<style lang="scss">
.banner-image {
  height: 100%;
  width: 100%;
}
.banner-text {
  position: absolute;
  top: 45%;
  left: 30%;
  transform: translate(-50%, -50%);
}
.custom-rating-text {
  color: #38c172;
  font-size: 1.25rem;
}
</style>

<script>
// @ is an alias to /src
import StarRating from "vue-star-rating";

export default {
  name: "MovieCard",
  components: {},
  data: function() {
    return {};
  }
};
</script>