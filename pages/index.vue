<template>
  <div>
    <Navbar :searchQuery="searchQuery" @search="searchCats" />
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4 mt-8 mx-auto max-w-screen-md lg:max-w-screen-xl">
      <div v-for="cat in cats" :key="cat.id" class="bg-white rounded-xl shadow-lg border-2 border-gray-800/25">
        <div class="flex justify-center cursor-pointer">
          <img :src="cat.images[0].path" :alt="cat.name" class="h-64 w-full object-cover rounded-t-lg" @click="showCatDetails(cat)">
        </div>
        <div class="p-4">
          <h3 class="text-lg font-semibold">{{ cat.name }}</h3>
          <p class="text-gray-500">{{ cat.breed }}</p>
          <p class="text-gray-500">{{ cat.age }} years old</p>
        </div>
      </div>
    </div>

    <Spinner v-if="isLoading" />
    <cat-detail-pop-up v-if="showPopup" @close="closeCatDetails" :cat="selectedCat" />
  </div>
</template>

<script>
import CatDetailPopUp from '@/components/CatDetailPopUp.vue';
import Spinner from '@/components/Spinner.vue';
import Navbar from '@/components/Navbar.vue';

export default {
  name: 'IndexPage',
  components: {
    CatDetailPopUp,
    Spinner,
    Navbar
  },
  data() {
    return {
      cats: [],
      searchQuery: '',
      showPopup: false,
      selectedCat: null,
      currentPage: 1,
      totalPages: 1,
      isLoading: false,
    };
  },
  mounted() {
    this.loadCats();
    window.addEventListener('scroll', this.handleScroll);
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    searchCats(val) {
      this.searchQuery = val;
      this.currentPage = 1;
      this.totalPages = 1;
      this.cats = [];
      this.loadCats();
    },
    async loadCats() {
      try {
        if (this.currentPage > this.totalPages) return;
        this.isLoading = true;
        const query = this.searchQuery.toLowerCase().trim();
        const response = await this.$axios.$get(
          `https://developer.redcomm.co.id/test/fe/test-api/api/cats/search?page=${this.currentPage}&search=${query}`
        );
        const { data } = response;

        const uniqueCats = data.data.filter(newCat => !this.cats.find(cat => cat.id === newCat.id));
        this.cats = [...this.cats, ...uniqueCats];
        this.currentPage = Number(data.meta.current_page) + 1;
        this.totalPages = Number(data.meta.total_pages);
        this.isLoading = false;
      } catch (error) {
        console.error('Failed to load cats:', error);
        this.isLoading = false;
      }
    },
    handleScroll() {
      const scrollHeight = document.documentElement.scrollHeight;
      const scrollTop = document.documentElement.scrollTop;
      const clientHeight = document.documentElement.clientHeight;
      const bottomOffset = 20;

      if (scrollTop + clientHeight >= scrollHeight - bottomOffset) {
        this.loadCats();
      }
    },
    showCatDetails(cat) {
      this.selectedCat = cat;
      this.showPopup = true;
    },
    closeCatDetails() {
      this.showPopup = false;
    },
    loadMoreCats() {
      if (this.$infiniteLoading.state.complete) {
        return;
      }

      if (this.currentPage < this.totalPages) {
        const nextPage = this.currentPage + 1;
        this.loadCats(nextPage);
      } else {
        this.$infiniteLoading.state.complete();
      }
    },
  },
};
</script>
