<template>
  <div>
    <div class="searchBar">
      <van-row>
        <van-col :span="3">
          <img
            :src="locationIcon"
            alt
            srcset
            width="75%"
            class="locationIcon"
          />
        </van-col>
        <van-col :span="16">
          <input
            type="text"
            name
            class="searchInput"
          />
        </van-col>
        <van-col :span="5">
          <van-button
            size="mini"
            class
          >查找</van-button>
        </van-col>
      </van-row>
    </div>
    <!--swiper area-->
    <div class="swiperArea">
      <van-swipe
        :autoplay="2000"
        indicator-color="white"
      >
        <van-swipe-item
          v-for="(item, index) of bannerPicArray"
          :key="index"
        >
          <img
            v-lazy="item.image"
            alt=""
            width="100%"
          >
        </van-swipe-item>
      </van-swipe>
    </div>
    <!--type bar-->
    <div class="typeBar">
      <div
        v-for="(item, index) in category"
        :key="index"
      >
        <img
          v-lazy="item.image"
          width="90%"
        >
        <span>{{ item.mallCategoryName }}</span>
      </div>
    </div>
    <!--adbanner area-->
    <div>
      <img
        v-lazy="adBanner"
        alt=""
        width="100%"
      >
    </div>
    <!--Recommend goods area-->
    <div class="recommendArea">
      <div class="recommendTitle">
        商品推荐
      </div>
      <div class="recommendBody">
        <!--swiper-->
        <swiper :options="swiperOption">
          <swiper-slide
            v-for="(item, index) in recommendGoods"
            :key="index"
          >
            <div class="recommendItem">
              <img
                :src="item.image"
                alt=""
                srcset=""
                width="80%"
              />
              <div>{{ item.goodsName }}</div>
              <div>￥{{ item.price | moneyFilter }} (￥{{ item.mallPrice | moneyFilter }})</div>
            </div>
          </swiper-slide>
        </swiper>
      </div>
    </div>

    <floorComponent
      :floorData="floor1"
      :floorTitle="floorName.floor1"
    />
    <floorComponent
      :floorData="floor2"
      :floorTitle="floorName.floor2"
    />
    <floorComponent
      :floorData="floor3"
      :floorTitle="floorName.floor3"
    />

    <!--Hot Area-->
    <div class="hotArea">
      <div class="hotTitle">热卖商品</div>
      <div class="hotGoods">
        <!--这里需要一个list组件-->
        <van-list>
          <van-row gutter="20">
            <van-col
              :span="12"
              v-for="(item, index) in hotGoods"
              :key="index"
            >
              <goods-info :goodsImage="item.image" :goodsName="item.name" :goodsPrice="item.price" />
            </van-col>
          </van-row>

        </van-list>
      </div>
    </div>

  </div>
</template>

<script>
import axiso from "axios";

import "swiper/dist/css/swiper.css";
import { swiper, swiperSlide } from "vue-awesome-swiper";
import floorComponent from "../component/floorComponent";

import { toMoney } from "@/filter/moneyFileter.js";
import goodsInfo from '../component/goodsInfoComponent'
import url from '@/serviceAPI.config.js'

export default {
  data() {
    return {
      msg: "Shopping Mall",
      locationIcon: require("../../assets/images/location.png"),
      bannerPicArray: [
        // {imageUrl: 'http://img14.360buyimg.com/babel/s590x470_jfs/t1/83093/14/11496/100667/5d8d6929E72060ad5/e6f1e3d510416416.jpg.webp'},
        // {imageUrl: 'http://img30.360buyimg.com/pop/s590x470_jfs/t1/78220/32/2466/86863/5d0b580dE4e2ef529/c30231955e943913.jpg.webp'},
        // {imageUrl: 'http://img12.360buyimg.com/pop/s590x470_jfs/t1/48172/9/11396/31866/5d85cde3Ef6551434/756f685a36e153ca.jpg.webp'}
      ],
      category: [],
      adBanner: "",
      recommendGoods: [],
      swiperOption: {
        slidesPerView: 3
      },
      floor1: [],
      floor2: [],
      floor3: [],
      floorName: {},
      hotGoods: [] //热卖商品
    };
  },
  filters: {
    moneyFilter(money) {
      return toMoney(money);
    }
  },
  components: {
    swiper,
    swiperSlide,
    floorComponent,
    goodsInfo
  },
  created() {
    axiso({
      url: url.getShopingMallInfo,
      method: "get"
    })
      .then(response => {
        console.log(response);
        if (response.status === 200) {
          this.category = response.data.category;
          this.adBanner = response.data.advertesPicture.PICTURE_ADDRESS;
          this.bannerPicArray = response.data.slides;
          // console.log(this.bannerPicArray);
          this.recommendGoods = response.data.recommend;
          this.floor1 = response.data.floor1;
          this.floor2 = response.data.floor2;
          this.floor3 = response.data.floor3;
          this.floorName = response.data.floorName;
          this.hotGoods = response.data.hotGoods;
        }
      })
      .catch(error => {
        console.log(error);
      });
  }
};
</script>

<style scoped>
.searchBar {
  height: 2.2rem;
  background-color: #e5017d;
  line-height: 2.2rem;
  overflow: hidden;
}
.searchInput {
  width: 100%;
  height: 1.3rem;
  border-top: 0px;
  border-left: 0px;
  border-right: 0px;
  border-bottom: 1px solid #fff !important;
  background-color: #e5017d;
  color: #fff;
}
.locationIcon {
  padding-top: 0.2rem;
  padding-left: 0.3rem;
}

.typeBar {
  background-color: #fff;
  margin: 0 0.3rem 0.3rem 0.3rem;
  border-radius: 0.3rem;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
}

.typeBar div {
  padding: 0.3rem;
  font-size: 12px;
  text-align: center;
}

.recommendArea {
  background-color: #fff;
  margin-top: 0.3rem;
}
.recommendTitle {
  border-bottom: 1px solid #eee;
  font-size: 14px;
  padding: 0.2rem;
  color: #e5017d;
}

.recommendBody {
  border-bottom: 1px solid #eee;
}
.recommendItem {
  width: 99%;
  border-right: 1px solid #eee;
  font-size: 12px;
  text-align: center;
}

.floorAnomaly {
  display: flex;
  flex-direction: row;
  background-color: #fff;
  border-bottom: 1px solid #ddd;
}
.floorAnomaly div {
  width: 10rem;
  box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.floorOne {
  border-right: 1px solid #ddd;
}
.floor-two {
  border-bottom: 1px solid #ddd;
}

.floorRule {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  background-color: #fff;
}

.floorRule div {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  width: 10rem;
  border-bottom: 1px solid #ddd;
}

.floorRule div:nth-child(odd) {
  border-right: 1px solid #ddd;
}

.hotArea {
  text-align: center;
  font-size: 14px;
  height: 1.8rem;
  line-height: 1.8rem;
}
</style>