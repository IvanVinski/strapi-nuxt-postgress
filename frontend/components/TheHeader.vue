<template>
  <div>
    <nav class="flex px-4 border-b shadow-lg items-center relative">
      <img src="icon.png" class="h-12 mr-3" alt="Movies Logo" />
      <div class="text-lg font-bold md:py-0 py-4">{{ $t("Movies") }}</div>
      <ul
        class="md:px-2 ml-auto flex md:space-x-2 relative top-full left-0 right-0"
      >
        <li class="relative parent">
          <a
            href="#"
            class="flex justify-between md:inline-flex p-4 items-center hover:bg-gray-50 space-x-2"
          >
            <span>{{ $t("Language") }}</span>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="w-4 h-4 fill-current pt-1"
              viewBox="0 0 24 24"
            >
              <path
                d="M0 7.33l2.829-2.83 9.175 9.339 9.167-9.339 2.829 2.83-11.996 12.17z"
              />
            </svg>
          </a>
          <ul
            class="child transition duration-300 absolute top-full right-0 w-48 bg-white shadow-lg rounded-b"
          >
            <li v-for="(locale, index) in availableLocales" :key="index">
              <nuxt-link
                class="flex px-4 py-3 hover:bg-gray-50 gap-4"
                :to="switchLocalePath(locale.code)"
              >
                <country-flag :country="locale.flag" />
                <span class="self-end">{{ locale.name }}</span>
              </nuxt-link>
            </li>
          </ul>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  computed: {
    availableLocales() {
      return this.$i18n.locales.filter((i) => i.code !== this.$i18n.locale);
    },
  },
};
</script>

<style>
.parent:hover .child {
  opacity: 1;
  height: auto;
  overflow: none;
  transform: translateY(0);
}
.child {
  opacity: 0;
  height: 0;
  overflow: hidden;
  transform: translateY(-10%);
}
</style>
