<template>
  <div class="snow-wrapper">
    <SnowFlake
      v-for="(item, index) of snowList"
      :option="item"
      :key="index"
      @showPhoto="showPhoto"
    />
    <PhotoBox
      v-if="photoBoxShow"
      :url="showPhotoUrl"
      @closePhotoBox="closePhotoBox"
    />
  </div>
</template>

<script>
import { photoList } from "./photoList";
import { randomMath } from "@/fun/common";

export default {
  name: "Snow",
  data() {
    return {
      timer: null,
      photoList,
      snowList: [],
      photoBoxShow: false,
      showPhotoUrl: "",
    };
  },
  components: {
    SnowFlake: () => import("./components/SnowFlake.vue"),
    PhotoBox: () => import("@/components/PhotoBox.vue"),
  },
  methods: {
    addCircle() {
      this.snowList.push({
        url: this.photoList[randomMath(0, this.photoList.length - 1)].url,
      });
    },
    showPhoto(url) {
      this.photoBoxShow = true;
      this.showPhotoUrl = url;
    },
    closePhotoBox() {
      this.photoBoxShow = false;
      this.showPhotoUrl = "";
    },
    randomMath(min, max) {
      return randomMath(min, max);
    },
  },
  mounted() {
    if (this.timer) {
      clearInterval(this.timer);
      this.timer = null;
    }
    this.addCircle();
    this.timer = setInterval(this.addCircle, 1000);
  },
  beforeDestroy() {
    if (this.timer) {
      clearInterval(this.timer);
      this.timer = null;
    }
  },
};
</script>

<style lang="less" scoped>
.snow-wrapper {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  background: #258dd2;
  position: relative;
}
</style>
