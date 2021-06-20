<template>
  <div class="h-screen flex flex-col">
    <Nuxt></Nuxt>
    <Search></Search>
  </div>
</template>

<script>
import Search from "../components/search.vue";
export default {
  components: {
    Search
  }
};
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
</style>
