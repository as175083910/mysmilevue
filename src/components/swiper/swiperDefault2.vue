<template>
  <div>
    <swiper :options="swiperOption">
      <swiper-slide
        class="swiperSlide"
        v-for="(item, index) in slide"
        :key="index"
      >
        Slide {{ item }}
      </swiper-slide>
              <div
          class="swiperPagination"
          slot="pagination"
        ></div>
    </swiper>
  </div>
</template>

<script>
import "swiper/dist/css/swiper.css";
import { swiper, swiperSlide } from "vue-awesome-swiper";
export default {
  data() {
    return {
      slide: [1, 2, 3, 4, 5, 6],
      swiperOption: {
        pagination: {
          el: ".swiperPagination",
          clickable: true,
        },
        loop: true
      }
    };
  },
  components: {
    swiper,
    swiperSlide
  }
};
</script>

<style scoped>
.swiperSlide {
  height: 4rem;
  text-align: center;
  padding-top: 3rem;
  border-bottom: 1px solid #ccc;
}
.swiperPagination {
    text-align: center;
}
</style>