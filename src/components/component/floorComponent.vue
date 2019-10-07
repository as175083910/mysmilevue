<template>
  <div>
    <div class="floor">
      <div class="floorTitle">{{ floorTitle }}</div>
      <div class="floorAnomaly">
        <div class="floorOne">
          <img
            :src="floorData0.image"
            alt=""
            srcset=""
            width="100%"
          >
        </div>
        <div>

          <div class="floorTwo">
            <img
              :src="floorData1.image"
              alt=""
              srcset=""
              width="100%"
            >
          </div>

          <div>
            <img
              :src="floorData2.image"
              alt=""
              srcset=""
              width="100%"
            >
          </div>

        </div>
      </div>
      <div class="floorRule">
        <div
          v-for="(item, index) in floorData.slice(1)"
          :key="index"
        >
          <img
            :src="item.image"
            alt=""
            srcset=""
            width="100%"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["floorData", "floorTitle"],
  data() {
    return {
      floorData0: {},
      floorData1: {},
      floorData2: {}
    };
  },
  created() {
    //none things
  },
  watch: {
    floorData() {
      console.log(this.floorData);
      this.floorData0 = this.floorData[0];
      this.floorData1 = this.floorData[1];
      this.floorData2 = this.floorData[2];
    }
  }
};
</script>

<style scoped>
.floorTitle {
    text-align: center;
    font-size: 14px;
    height: 1.8rem;
    line-height: 1.8rem;
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
</style>