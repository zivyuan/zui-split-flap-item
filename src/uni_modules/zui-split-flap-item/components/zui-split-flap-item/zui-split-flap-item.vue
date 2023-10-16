<template>
  <view class="zui-split-flap-item">
    <view class="zui-split-flap-item-wrapper" :style="style">
      <view class="zui-split-flap-item-base">
        <img
          src="../../assets/zui-split-flap-item-base.png"
          :width="sizes.width"
          :height="sizes.height"
        />
      </view>
      <zui-split-flap-item-char
        position="top"
        :char="topChar"
        :width="sizes.charWidth"
        :height="sizes.charHeight"
        :duration="duration"
      />
      <zui-split-flap-item-char
        layer="animate"
        position="top"
        :char="topCharFlip"
        :width="sizes.charWidth"
        :height="sizes.charHeight"
        :duration="duration"
      />
      <zui-split-flap-item-char
        position="bottom"
        :char="bottomChar"
        :width="sizes.charWidth"
        :height="sizes.charHeight"
        :duration="duration"
      />
      <zui-split-flap-item-char
        layer="animate"
        position="bottom"
        :char="bottomCharFlip"
        :width="sizes.charWidth"
        :height="sizes.charHeight"
        :duration="duration"
      />
    </view>
  </view>
</template>

<script>
import ZuiSplitFlapItemChar from "./zui-split-flap-item-char.vue";

export default {
  name: "zui-split-flap-item",

  components: {
    ZuiSplitFlapItemChar,
  },

  props: {
    char: { type: [String, Number], default: "0" },
    size: { type: Number, default: 32 },
    color: { type: String, default: "#333" },
    font: { type: String, default: '"Robot", "monospace", "DIN Condensed"' },
    // 延迟
    delay: { type: Number, default: 0 },
    duration: { type: Number, default: 400 },
  },

  data() {
    return {
      // duration: 400,
      prevChar: '0',
      flip: false,
      topChar: this.char,
      topCharFlip: '',
      bottomChar: '',
      bottomCharFlip: this.char,
    };
  },

  watch: {
    char(n, o) {
      if (this.delay) {
        setTimeout(() => {
          this.updateChars(n, o)
        }, this.delay)
      } else {
        this.updateChars(n, o)
      }
    }
  },

  computed: {
    sizes() {
      const outerRatio = 1.81437126;
      const charWidRatio = 0.91742515;
      const charHeiRatio = 0.9007245;

      return {
        width: Math.round(this.size),
        height: Math.round(this.size * outerRatio),
        charWidth: Math.round(this.size * charWidRatio),
        charHeight: Math.round(this.size * charWidRatio * charHeiRatio),
      };
    },
    style() {
      const style = {
        "--zui-split-flap-item-width": `${this.sizes.width}px`,
        "--zui-split-flap-item-height": `${this.sizes.height}px`,
        "--zui-split-flap-item-char-width": `${this.sizes.charWidth}px`,
        "--zui-split-flap-item-char-height": `${this.sizes.charHeight}px`,
        "--zui-split-flap-item-char-color": this.color,
        "--zui-split-flap-item-char-size": `${this.sizes.charWidth * 0.6}px`,
        "--zui-split-flap-item-duration": this.duration + 'ms',
        "--zui-split-flap-item-duration-half": (this.duration / 2) + 'ms',
        "--zui-split-flap-item-char-font": this.font,
      };

      return Object.keys(style)
        .map((key) => `${key}: ${style[key]}`)
        .join(";");
    },
  },

  methods: {
    updateChars(n, o) {
      this.topChar = n
      this.topCharFlip = o
      this.bottomChar = o
      this.bottomCharFlip = n
    }
  },
};
</script>

<style scoped lang="scss">
.zui-split-flap-item {
  display: inline-block;
  width: var(--zui-split-flap-item-width);
  height: var(--zui-split-flap-item-height);
  line-height: 0;
}

.zui-split-flap-item-wrapper {
  position: relative;
  perspective: 180px; // 240
}

// .zui-split-flap-item-base {

// }
</style>
