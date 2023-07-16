<template>
  <div class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50" @click="handleBackgroundClick($event)">
    <div class="bg-white rounded-lg max-w-xl" @click.stop>
      <div class="relative flex items-center justify-between px-4 py-2 bg-gray-800 rounded-t-lg">
        <h2 class="text-xl font-semibold text-white">{{ cat.name }}</h2>
        <button class="absolute top-0 right-0 mt-3 mr-3 focus:outline-none" @click="closePopup">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
          </svg>
        </button>
      </div>
      <div class="swiper-container mb-2" ref="swiperContainer">
        <div class="swiper-wrapper">
          <div v-for="(image, index) in cat.images" :key="image.id" class="swiper-slide">
            <img :src="image.path" :alt="'Cat Image ' + index" class="object-cover w-full h-full">
          </div>
        </div>
        <div class="swiper-pagination"></div>
      </div>
      <div class="p-4">
        <h3 class="text-lg font-semibold">{{ cat.name }}</h3>
        <p class="text-gray-500">Age: {{ cat.age }}</p>
        <p class="text-gray-500">Breed: {{ cat.breed }}</p>
        <p class="text-gray-500">Color: {{ cat.color }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import Swiper, { Pagination } from 'swiper';
import 'swiper/swiper-bundle.css';

export default {
  props: {
    cat: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      swiper: null,
    };
  },
  mounted() {
    Swiper.use([Pagination]);
    this.$nextTick(() => {
      this.initializeSwiper();
    });
  },
  beforeUnmount() {
    if (this.swiper) {
      this.swiper.destroy();
    }
  },
  methods: {
    initializeSwiper() {
      this.swiper = new Swiper(this.$refs.swiperContainer, {
        slidesPerView: 'auto',
        centeredSlides: true,
        spaceBetween: -30,
        loop: true,
        loopedSlides: this.cat.images.length,
        pagination: {
          el: '.swiper-pagination',
          clickable: true,
        },
      });
    },
    handleBackgroundClick(event) {
      if (event.target === this.$el) {
        this.closePopup();
      }
    },
    closePopup() {
      this.$emit('close');
    },
  },
};
</script>

<style scoped>
.swiper-container {
  width: 100%;
  height: 20rem;
  overflow: hidden;
}

.swiper-slide {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.swiper-slide img {
  width: 100%;
  height: 20rem;
  object-fit: cover;
  object-position: center;
  max-width: 100%;
  max-height: 100%;
  opacity: 1;
  transition: opacity 0.3s ease;
}

.swiper-slide-next,
.swiper-slide-prev {
  pointer-events: none;
}

.swiper-slide-next img,
.swiper-slide-prev img {
  opacity: 0;
  transition: opacity 0.3s ease;
}

.swiper-slide-active img {
  opacity: 1;
}
</style>
