<template>
  <div>
    <Slide push>
      <h1 class="text-green text-3xl text-left p-0 m-0">MovieTime</h1>
      <router-link to="/">
        <span>Home</span>
      </router-link>
      <router-link to="/search">
        <span>Search</span>
      </router-link>
      <router-link to="/about">
        <span>About</span>
      </router-link>
      <!-- <router-link to="/pricing">
        <span>Pricing</span>
      </router-link>-->
    </Slide>
  </div>
</template>

<style lang="scss">
.bm-burger-bars {
  background-color: #38c172;
  z-index: 100;
}

.bm-menu {
  background-color: #3d4852;
}

.bm-item-list {
  color: #f8fafc;
}

.router-link-exact-active span {
  color: #38c172;
}
</style>

<script>
import { Slide } from "vue-burger-menu";

export default {
  name: "navbar",
  components: {
    Slide
  }
};
</script>
