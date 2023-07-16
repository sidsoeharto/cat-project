<template>
  <nav class="navbar sticky bg-gray-800 top-0 z-10">
    <div class="container mx-auto px-4 py-2 flex items-center justify-between">
      <div class="mr-auto flex items-center">
        <nuxt-link
          exact
          class="text-white font-semibold text-lg mr-4 py-2 hover:text-green-400"
          to="/"
          active-class="text-green-400"
        >
          Cats
        </nuxt-link>
        <nuxt-link
          class="text-white font-semibold text-lg py-2 hover:text-green-400"
          to="/create-cat"
          active-class="text-green-400"
        >
          Add Cat
        </nuxt-link>
      </div>
      <div class="ml-auto flex items-center">
        <div v-if="showSearch" class="relative">
          <input
            type="text"
            v-model="inputVal"
            placeholder="Search cats..."
            class="bg-gray-700 text-white rounded-full px-8 py-2 w-48 md:w-64 lg:w-96 focus:outline-none"
          />
          <span class="absolute right-3 top-2 text-gray-500">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
              <path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z" />
            </svg>
          </span>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  props: {
    searchQuery: {
      type: String
    },
    showSearch: {
      type: Boolean,
      default: true,
    },
  },
  computed: {
    inputVal: {
      get() {
        return this.searchQuery;
      },
      set(val) {
        this.$emit('search', val);
      }
    }
  },
};
</script>

<style scoped>
</style>
