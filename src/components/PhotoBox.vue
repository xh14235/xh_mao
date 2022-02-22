<template>
  <div class="photo-box" @click="closePhotoBox">
    <div
      class="img-box"
      :style="{ transform: `rotate(${randomMath(-15, 15)}deg)` }"
    >
      <img :src="require('@/assets/images/' + url + '.jpg')" alt="" />
    </div>
  </div>
</template>

<script>
import { randomMath } from "@/fun/common";

export default {
  name: "PhotoBox",
  props: {
    url: String,
  },
  methods: {
    closePhotoBox() {
      this.$emit("closePhotoBox");
    },
    randomMath(min, max) {
      return randomMath(min, max);
    },
  },
};
</script>

<style lang="less" scoped>
.photo-box {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  z-index: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  .img-box {
    max-width: 60%;
    max-height: 80%;
    padding: 16px;
    background: #fff;
    transform: rotate(-15deg);
    img {
      max-width: 100%;
      max-height: 80vh;
    }
  }
}
</style>
