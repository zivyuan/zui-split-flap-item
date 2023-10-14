<template>
  <view :class="['zui-split-flap-item-char', position, layer, animate]">
    <img v-if="position === 'top'" src="../../assets/zui-split-flap-item-top.png" :width="width" :height="height" />
    <img v-if="position === 'bottom'" src="../../assets/zui-split-flap-item-bottom.png" :width="width" :height="height" />
    <view class="zui-split-flap-item-char-text">{{ char }}</view>
    <view class="zui-split-flap-item-char-shadow"></view>
  </view>
</template>

<script>

/**
 *
 *  pagename
 *
 */
export default {
  name: 'zui-split-flap-item-char',

  components: {},

  props: {
    layer: {
      type: String,
      // 'char' | 'animate'
      default: 'char',
    },

    char: {
      type: [String, Number],
      default: '0',
    },

    width: {
      type: Number,
      required: true,
    },

    height: {
      type: Number,
      required: true,
    },

    position: {
      type: String,
      default: 'top',
    },

    duration: {
      type: Number,
      default: 600,
    }
  },

  data() {
    return {
      // 动画时长
      prevChar: '0',
      animate: this.layer === 'animate' ? 'animate-flip' : '',
    }
  },

  watch: {
    char(n, o) {
      if (this.layer !== 'animate') return

      this.animate = ''
      setTimeout(() => {
        this.animate = 'animate-flip'
      }, 30)
    }
  },

  methods: {},
}
</script>

<style lang="scss" scoped>
.zui-split-flap-item-char {
  position: absolute;
  z-index: 5;
  left: 50%;
  top: 50%;
  width: var(--zui-split-flap-item-char-width);
  height: var(--zui-split-flap-item-char-height);
  overflow: hidden;
}

.zui-split-flap-item-char-text,
.zui-split-flap-item-char-shadow {
  position: absolute;
  left: 0;
}

.zui-split-flap-item-char-text {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  // height: calc(var(--zui-split-flap-item-char-height) * 2);
  font-size: calc(var(--zui-split-flap-item-char-width));
  font-weight: bold;
  color: var(--zui-split-flap-item-char-color);
  font-family: var(--zui-split-flap-item-char-font);
  display: flex;
  justify-content: center;
  align-items: center;
  line-height:  0; //calc(var(--zui-split-flap-item-char-height) * 2);
}

.top,
.bottom {
  z-index: 5;
  transition-duration: 0s;
  transition-property: transform, display;
}

.top {
  transform-origin: center bottom;
  transform: translate(-50%, -102%) rotateX(360deg);

  .zui-split-flap-item-char-text {
    bottom: 0;
    transform: translateY(58%);
  }
}

.bottom {
  transform-origin: center top;
  transform: translate(-50%, 2%) rotateX(360deg);
  transition-delay: var(--zui-split-flap-item-duration-half);

  .zui-split-flap-item-char-text {
    top: 0;
    transform: translateY(-45%);
  }
}

.animate {
  &.top {
    transform: translate(-50%, -102%) rotateX(360deg);
  }

  &.bottom {
    transform: translate(-50%, 2%) rotateX(450deg);
    transition-delay: 0s;
  }
}

.animate-flip {
  &.top {
    transform: translate(-50%, -102%) rotateX(270deg);
    transition-duration: var(--zui-split-flap-item-duration-half);
  }
  &.bottom {
    transform: translate(-50%, 2%) rotateX(360deg);
    transition-duration: var(--zui-split-flap-item-duration-half);
    transition-delay: var(--zui-split-flap-item-duration-half);
  }
}
</style>