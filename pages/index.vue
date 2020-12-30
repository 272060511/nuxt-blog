<template>
  <div class="container home-page">
    <home-header/>
    <div class="home-article-list">
      <home-articles :datas="articleDatas" :isLoading="isLoading" :isNext="isNext"/>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Home',
  data() {
    return {
      articleDatas: [],
      isLoading: false,
      isNext: true
    }
  }
}
</script>

<style lang="scss">
.container {
  overflow: hidden;
  .home-article-list{
    width: 1200px;
    margin: auto;
    text-align: center;
    padding: 80px 0;
    position: relative;
    &::after {
      content: '';
      left: 50%;
      transform: translateX(-50%);
      top: 0;
      position: absolute;
      background: #eaeaea;
      z-index: 0;
      width: 1px;
      height: 100%;
    }
  }
}

</style>
