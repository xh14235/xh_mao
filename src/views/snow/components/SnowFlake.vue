<template>
  <div
    class="snow-flake-box"
    :style="{ left: snowLeft + 'px' }"
    @click="showPhoto(option.url)"
  >
    <img
      :class="[`rotate${random}`]"
      :src="require('@/assets/icons/snow' + randomMath(1, 5) + '.png')"
    />
  </div>
</template>

<script>
import { randomMath } from "@/fun/common";

export default {
  name: "SnowFlake",
  data() {
    return {
      random: 0,
    };
  },
  props: {
    option: Object,
  },
  computed: {
    snowLeft() {
      const w = document.body.clientWidth - 32;
      const l = Math.floor(Math.random() * (w + 1));
      return l;
    },
  },
  methods: {
    randomMath(min, max) {
      return randomMath(min, max);
    },
    showPhoto(url) {
      this.$emit("showPhoto", url);
    },
  },
  created() {
    this.random = randomMath(0, 1);
  },
};
</script>

<style lang="less" scoped>
.snow-flake-box {
  width: 32px;
  height: 32px;
  animation: down 30s linear forwards;
  position: absolute;
  top: -32px;
  .rotate1 {
    animation: rotate1 30s linear;
  }
  .rotate0 {
    animation: rotate0 30s linear;
  }
}

@keyframes down {
  0% {
    transform: translateY(-32px);
  }
  100% {
    transform: translateY(calc(100vh + 16px));
  }
}

@keyframes rotate1 {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes rotate0 {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(-360deg);
  }
}
</style>
