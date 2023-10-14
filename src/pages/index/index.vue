<template>
  <view class="content">
    <view class="demo-header">
      <image class="logo" src="/static/logo.png"></image>
      <text class="title">&lt;{{ title }} /&gt;</text>
    </view>

    <view class="demo-container">
      <zui-split-flap-item :char="chars[0]" />
      <zui-split-flap-item :char="chars[1]" />
      <text class="colon">:</text>
      <zui-split-flap-item :char="chars[2]" />
      <zui-split-flap-item :char="chars[3]" />
      <text class="colon">:</text>
      <zui-split-flap-item :char="chars[4]" />
      <zui-split-flap-item :char="chars[5]" />
    </view>
    <view class="demo-container">
      <zui-split-flap-item :char="airport[0]" />
      <zui-split-flap-item :char="airport[1]" :delay="200" />
      <zui-split-flap-item :char="airport[2]" :delay="400" />
      <zui-split-flap-item :char="airport[3]" :delay="600" />
      <zui-split-flap-item :char="airport[4]" :delay="800" />
      <zui-split-flap-item :char="airport[5]" :delay="1000" />
    </view>
  </view>
</template>

<script>
import ZuiSplitFlapItem from "../../uni_modules/zui-split-flap-item/components/zui-split-flap-item/zui-split-flap-item.vue";
export default {
  components: {
    ZuiSplitFlapItem,
  },
  data() {
    return {
      title: "zui-split-flap-item",
      chars: [0, 0, 0, 0, 0, 0],
      count: 0,
      clockIId: 0,

      airport: "abcdef",
      airportIId: 0,
    };
  },
  onLoad() {},

  onShow() {
    this.clockStart();
    this.updateAirport();
  },

  onHide() {
    this.clockStop();
    this.stopUpdateAirport();
  },

  methods: {
    clockStart() {
      this.clockStop();

      const date = new Date();
      const hou = ("0" + date.getHours()).slice(-2);
      const min = ("0" + date.getMinutes()).slice(-2);
      const sec = ("0" + date.getSeconds()).slice(-2);

      this.chars = `${hou}${min}${sec}`.split("");
      // this.chars = `AMgi09`.split('')
      this.clockIId = setTimeout(() => {
        this.clockStart();
      }, 1000);
    },

    clockStop() {
      clearTimeout(this.clockIId);
    },

    updateAirport() {
      this.stopUpdateAirport()

      const ap = [
        "ZBDT",
        "ZUDX",
        "ZUDC",
        "ZYDD",
        "ZPDQ",
        "ZYTL",
        "ZPDL",
        "ZLDH",
        "ZSDY",
        "ZYDQ",
        "ZBDS",
        "ZGDY",
        "ZHEC",
        "ZHES",
        "ZLYA",
        "ZBER",
        "ZSFA",
        "ZGFS",
        "ZSFZ",
        "ZSFY",
        "ZYFY",
        "ZWFY",
        "ZUGH",
        "ZLGM",
        "ZUGU",
      ];
      const na = ["AF", "AL", "ZH", "CN", "US", "EN"];

      this.airport =
        na[Math.floor(Math.random() * na.length)] +
        ap[Math.floor(Math.random() * na.length)];

      this.airportIId = setTimeout(() => {
        this.updateAirport()
      }, 5000)
    },

    stopUpdateAirport() {
      clearTimeout(this.airportIId)
    }
  },
};
</script>

<style>
.content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.demo-header {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  width: 100%;
  padding: 32rpx;
  box-sizing: border-box;
}

.logo {
  height: 64rpx;
  width: 64rpx;
  margin-right: 32rpx;
}

.title {
  font-size: 36rpx;
  color: #8f8f94;
}

.demo-container {
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 32rpx;

  .colon {
    font-family: "Robot", "monospace", "DIN Condensed";
    font-size: 48rpx;
    font-weight: bold;
    margin: 0 8rpx;
  }
}

.zui-split-flap-item {
  margin: 0 6rpx;
}
</style>
