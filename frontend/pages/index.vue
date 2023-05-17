<template>
  <div class="m-5">
    <div class="flex justify-center">
      <div class="flex flex-col gap-10 w-full md:w-3/4 lg:w-2/3">
        <div class="text-6xl">{{ $t("ListOfMovies") }}</div>
        <ul>
          <li class="flex gap-10 m-5" v-for="movie in movies">
            <img
              :src="`${$config.apiURL}${movie.attributes.image.data.attributes.url}`"
              class="h-60"
            />
            <div class="flex flex-col gap-5">
              <div class="text-4xl">{{ movie.attributes.name }}</div>
              <div class="text-lg">
                {{ movie.attributes.description }}
              </div>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "IndexPage",

  data: () => ({
    movies: [],
  }),

  async mounted() {
    // Get data from Strapi
    const response = await this.$axios.$get(
      `/api/movies?populate=*&locale=${this.$i18n.locale}`
    );

    this.movies = response.data;
  },
};
</script>
