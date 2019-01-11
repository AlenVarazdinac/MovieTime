<template>
  <div class="home bg-black mx-auto">
    <Banner/>
    <PopularMovies/>
    <LatestMovies/>
    <Footer/>
  </div>
</template>

<style lang="scss">
</style>


<script>
// @ is an alias to /src
import Banner from "@/components/Banner.vue";
import Footer from "@/components/Footer.vue";
import PopularMovies from "@/components/PopularMovies.vue";
import LatestMovies from "@/components/LatestMovies.vue";

export default {
  name: "home",
  components: {
    Banner,
    Footer,
    PopularMovies,
    LatestMovies
  }
};
</script>
