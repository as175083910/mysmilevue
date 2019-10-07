<template>
  <div>
    <swiper class="swiper" :options="swiperOption">
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
        direction: 'vertical',
        pagination: {
          el: ".swiperPagination"
        }
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
  line-height: 4rem;
}
.swiperPagination {
    text-align:center;
}
.swiper {
  height: 7rem;
  border-top: 1px solid #ccc;
  border-bottom: 1px solid #ccc;
}
</style>