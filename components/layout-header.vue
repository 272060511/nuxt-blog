<template>
  <div class="header">
    <div class="header-left">
      <img src="../static/image/logo-black.png" alt="" />
      <i
        class="iconfont"
        @click="changeMusic"
        :class="isPlay ? 'icon-zanting' : 'icon-bofang'"
      ></i>
    </div>
    <div class="header-right">
      <nuxt-link to="/"
        ><img src="../static/image/avatar.png" alt=""
      /></nuxt-link>
    </div>
    <div class="progressBar" :style="{width: progressBarWidth + '%'}"></div>
    <audio loop id="music">
      <source src="../static/music/wanghouyusheng.mp3">
    </audio>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isPlay: false,
      music: '',
      dashArray: Math.PI * 100,
      progressBarWidth: 0
    };
  },
  computed: {
    dashOffset() {
      return (1 - this.progressBarWidth / 100) * this.dashArray;
    }
  },
  mounted () {
    this.initMusic() // 加载音乐
  },
  methods: {
    changeMusic() {
      this.listenPlay()
      this.startListen = true
      !this.isPlay ? this.audioDom.play() : this.audioDom.pause()
      this.isPlay = !this.isPlay
    },
    // 第一次播放的时候开始监听
    listenPlay () {
      if (this.startListen) return
      this.audioDom.ontimeupdate =  () => {
        const currentTime = ( this.audioDom.currentTime / this.audioDom.duration * 100 ).toFixed(0)
        this.progressBarWidth = currentTime
      }
    },
    // 初始化音乐
    initMusic () {
      this.audioDom = document.getElementById("music")
      this.audioDom.load()
    },
  }
};
</script>

<style lang="scss">
.header {
  width: 100vw;
  height: 50px;
  position: fixed;
  z-index: 100;
  top: 0;
  left: 0;
  border-bottom: 1px solid #eeeeee;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 15px;
  .header-left {
    display: flex;
    align-items: center;
    img {
      display: block;
      width: 40px;
      height: auto;
      cursor: pointer;
      transition: all 0.2s;
      &:hover {
        animation: jump 1s infinite alternate;
      }
    }
    .iconfont {
      color: #888;
      margin-left: 20px;
      font-size: 22px;
      cursor: pointer;
      transition: all 0.3s;
      &:hover {
        color: #303033;
      }
    }
  }
  .header-right {
    img {
      display: block;
      width: 40px;
      height: auto;
      border: 1px solid #eeeeee;
      border-radius: 50%;
      &:hover{
        transform: rotate(666turn);
        transition-delay: 1s;
        transition-property: all;
        transition-duration: 59s;
        transition-timing-function: cubic-bezier(.34,0,.84,1);
      }
    }
  }
  .progressBar {
    position: absolute;
    top: 0;
    left: 0;
    width: 0;
    height: 50px;
    background-color: #eee;
    z-index: -1;
  }
  @keyframes jump {
    0% {
      transform: translateY(0px) scale(1);
    }
    60% {
      transform: translateY(2px) scale(1.1);
    }
    100% {
      transform: translateY(-4px) scale(1);
    }
  }
}
</style>
