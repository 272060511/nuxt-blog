<template>
  <div class="home-header" :class="{navActive: isActive}">
    <div id="scene" class="home-background-img">
      <div class="layer" data-depth="0.4">
        <img class="moveImg" src="../static/image/header-bg.jpg" alt="" :width="imgWidth" :height="imgHeight"/>
      </div>
    </div>
    <div class="head">
      <div class="logo-img">
        <nuxt-link to="/">
          <span class="iconfont icon-touxiang" :style="{ color: isActive ? 'black' : 'white' }"></span>
        </nuxt-link>
      </div>
      <div class="menu" @click="clickMenu">
        <span class="iconfont" :class="isActive ? 'icon-hebingxingzhuang' : 'icon-combinedshape'"></span>
      </div>
    </div>
    <div class="head-masking" :style="{ backgroundColor: personalSetting.maskColor }"></div>
    <div class="head-summary">
      <div class="time">{{ personalSetting.summary.time }}</div>
      <div class="title">
        <nuxt-link :to="personalSetting.summary.link">{{ personalSetting.summary.title }}</nuxt-link>
      </div>
      <div class="describe">{{ personalSetting.summary.describe }}</div>
    </div>
    <!-- nav menu -->
    <div class="nav-box">
      <ul class="nav-list">
        <li v-for="(item, index) in navSetting" :key="index">
          <nuxt-link :to="item.path"><span class="iconfont" :class="item.icon">{{ item.name }}</span></nuxt-link>
        </li>
        <li class="login-register-btn">
          <nuxt-link to="login"><span class="iconfont" :class="loginStatus === 1 ? 'icon-login' : 'icon-register'">{{ loginStatus=== 1 ? '登录' : '注册' }}</span></nuxt-link>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Parallax from "parallax-js";

export default {
  name: "HomeHeader",
  data() {
    return {
      bgImgStyle: "",
      isActive: false,
      personalSetting: {
        maskColor: "",
        summary: {
          time: "十二月，8号，2020年",
          title: "随记",
          describe: "2020年12月8日，阴转小雨。",
          link: "www.baidu.com",
        },
      },
      imgWidth: null,
      imgHeight: null,
      navSetting: [
        { name:' 主页',icon:'icon-home', path:'/' },
        { name:' 文章',icon:'icon-wenzhang', path:'article' },
        { name:' 听雨',icon:'icon-lingting', path:'/' },
        { name:' 留言',icon:'icon-liuyan', path:'/' },
        { name:' 关于我',icon:'icon-guanyu', path:'/' },
        { name:' Github',icon:'icon-github', path:'' },
      ],
      loginStatus: 0,
    };
  },
  mounted() {
    let wWidth = document.documentElement.clientWidth;
    let wHeight = document.documentElement.clientHeight;
    this.imgWidth = wWidth + 150;
    this.imgHeight = wHeight + 150;
    if (wWidth <= 600) {
      this.imgWidth = 1920 / 1.3;
      this.imgHeight = 960;
    }
    const scene = document.getElementById("scene");
    const parallaxInstance = new Parallax(scene, {
      relativeInput: true,
      clipRelativeInput: true,
    });
    this.getPesonalSettingDate();
  },
  methods: {
    getPesonalSettingDate() {
      const date = new Date();
      const year = date.getFullYear();
      const month = date.getMonth() + 1;
      const day = date.getDate();
      this.personalSetting.summary.time = month + "月，" + day + "日，" + year+'年';
    },
    clickMenu() {
      this.isActive = !this.isActive
    },
  },
};
</script>

<style lang="scss" scoped>
.home-header {
  width: 100vw;
  height: 100vh;
  position: relative;

  #scene {
    // height: 100%;
    position: relative;
    overflow: hidden;

    #image {
      position: absolute;
      max-width: none;
      display: block;
    }
  }

  .home-background-img {
    width: 100%;
    height: 100%;
    pointer-events: none;

    .layer {
      width: 100%;
      height: 100%;
    }

    .moveImg {
      margin-bottom: 20px;
      top: -50px;
      left: 50%;
      transform: translateX(-50%);
      position: absolute;
      max-width: none;
      display: block;
    }
  }

  .head {
    width: 100%;
    padding: 0 40px;
    color: #f2f2f2;
    z-index: 1001;
    position: absolute;
    top: 70px;
    display: flex;
    justify-content: space-between;
    align-items: center;

    .logo-img {
      a{
        display: block;
        height: 44px;
        line-height: 44px;
      }
      span {
        font-size: 40px;
        cursor: pointer;
        transition: all 0.4s;
        display: inline-block;
      }
    }

    .menu {
      width: 30px;
      height: 30px;
      line-height: 32px;
      border-radius: 2px;
      cursor: pointer;
      color: #ec6641;
      text-align: center;
      background: rgba(255, 255, 255, 0.9);

      span {
        font-size: 20px;
      }
    }
  }

  .head-masking {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(55, 199, 218, 0.6);
    clip-path: polygon(0 0, 25% 0, 60% 100%, 0% 100%);
  }

  .head-summary {
    position: absolute;
    top: 50%;
    left: 10%;
    color: #f2f2f2;
    width: 65%;
    transform: translateY(-50%);

    .time {
      font-size: 14px;
    }

    .title {
      margin: 15px 0 30px;

      a {
        font-size: 28px;
        color: #f2f2f2;
        text-decoration: none;
        cursor: pointer;
        transition: all 0.3s;

        &:hover {
          text-decoration: underline;
        }
      }
    }

    .describe {
      line-height: 22px;
    }
  }
  .nav-box{
    position: fixed;
    left: 0;
    top: -100%;
    width: 100%;
    height: 100%;
    z-index: 1000;
    display: flex;
    justify-content: center;
    align-items: center;
    animation: change 15s infinite ;
    background: linear-gradient(125deg,#2980b9,#633bd3,#8e44ad,#192f44,#27ae60);
    background-size: 800%;
    transition: top .3s cubic-bezier(.25, .5, .5, .9);
    .nav-list{
      width: 80%;
      display: flex;
      justify-content: space-around;
      flex-wrap: wrap;
      margin-top: -100px;
      li{
        margin: 0 20px;
      }
      a{
        cursor: pointer;
        color: #f2f2f2;
        letter-spacing: 1px;
        span{
          font-size: 24px;
        }
        &:hover{
          color: #eee;
        }
      }
    }
  }
   @keyframes change {
    0% { background-position-x: 0%;}
    50% { background-position-x: 100%; }
    100% { background-position-x: 0%;}
  }
}

@media screen and (max-width: 900px) {
  .home-header {
    .head-masking {
      clip-path: polygon(0 0, 220px 0, 700px 100%, 0% 100%);
    }
  }
}

@media screen and (max-width: 780px) {
  .home-header {
    .head {
      top: 40px;
      padding: 0 20px;
    }

    .head-masking {
      clip-path: none;
    }
     .nav-box{
       .nav-list{
        justify-content: space-around;
        li{
          width: 35%;
          line-height: 30px;
          margin: 0;
          span{
            font-size: 20px;
          }
        }
      }
     }
  }
}
.navActive {
  .nav-box{
		top: 0;
	}
}
</style>
