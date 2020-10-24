<template>
  <div>
  <div>
    <div class="gs-menu-bg"></div>
    <div class="gs-header">
      <div class="gs-quick-menu">
        <div class="gs-profile">
          <span>你好</span>&nbsp;&nbsp;&nbsp;&nbsp;
          <span>消息 <strong>0</strong></span>
        </div>
        <ul class="gs-nav">
          <li class="gs-nav-item">
            <router-link class="gs-link" to="/order">我的订单</router-link>
          </li>
          <li class="gs-nav-item">
            <router-link class="gs-link" to="/cart">
              <i class="fa fa-shopping-cart"></i>&nbsp;购物车
            </router-link>
          </li>
          <li class="gs-nav-item">
            <span class="gs-link gs-forbid">商家入口</span>
          </li>
        </ul>
      </div>
      <div>
        <div class="gs-logo" @click="toHomepage"></div>
        <div class="gs-search-box">
          <input
            class="gs-search-input"
            type="text"
            placeholder="请输入 商品/店铺"><!--
          --><span class="gs-search-btn">搜&nbsp;&nbsp;索</span>
        </div>
      </div>
    </div>
    <div class="gs-dividor"></div>
  </div>
  <div class="container">
    <div
      class="swiper-bg"
      :style="{backgroundColor: slidesColor[index]}"
    />
    <div class="stage">
      <ul class="category-nav">
        <li
          v-for="(item, index) in navbars"
          :key="index"
          class="cate-nav-item"
        >
          <i class="cate-nav-icon" :class="item.icon" />
          &nbsp;&nbsp;{{ item.text }}
        </li>
      </ul>
      <div class="swiper">
        <Swiper :slides="slidesImage" v-model="index"></Swiper>
      </div>
    </div>
    <div class="rec-banner">
      <h1 class="banner-title">精品推荐</h1>
      <ul class="rec-list">
        <li
          v-for="(item, index) in goods"
          :key="index"
          class="rec-card"
          @click="togglePage(item)"
        >
          <img class="rec-media" :src="item.cover">
          <div class="rec-profile">
            <h4>{{ item.text }}</h4>
            <p class="rec-params">
              原价: <span class="rec-price">￥{{ item.price }}</span>&nbsp;
              促销价: <span class="rec-online-price">￥{{ item.onlinePrice }}</span>
            </p>
          </div>
        </li>
      </ul>
    </div>
  </div>
  </div>
</template>

<script>
import Swiper from '@/components/Swiper'
import config from '@/config/config'
export default {
  name: 'Index',
  components: { Swiper },
  data() {
    return {
      index: 0
    }
  },
  computed: {
    navbars: function() {
      return config.navbars
    },
    goods() {
      return config.goods
    },
    slidesColor() {
      return config.goods.map(item => item.color)
    },
    slidesImage() {
      return config.goods.map(item => item.poster)
    }
  },
  methods: {
    togglePage(item) {
      this.$router.push({ path: '/goods', query: { name: item.name }})
    }
  }
}
</script>

<style scoped>
.container {
  position: relative;
  background-color: #f5f5f5;
  border-bottom: 1px solid transparent;
}
.swiper-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 500px;
  background-color: #e5e5e5;
}
.stage {
  width: 1120px;
  margin-left: auto;
  margin-right: auto;
  background-color: #789;
}
.category-nav {
  display: inline-block;
  position: absolute;
  width: 200px;
  height: 500px;
  z-index: 2;
  list-style: none;
  background-color: rgba(0, 0, 0, 0.55);
}
.cate-nav-item {
  padding-left: 12px;
  line-height: 35.7143px;
  color: #fff;
  cursor: pointer;
}
.cate-nav-item:hover {
  color: #787878;
  background-color: rgba(255, 255, 255, .8);
}
.cate-nav-icon {
  opacity: .5;
}
.swiper {
  height: 500px;
  background-color: #e8e8e8;
}
.rec-banner {
  margin: 30px auto;
  padding-top: 30px;
  padding-bottom: 50px;
  width: 1120px;
  background-color: #fff;
}
.banner-title {
  padding: 8px 15px;
}
.rec-list {
  list-style: none;
}
.rec-card {
  display: inline-block;
  width: 25%;
  text-align: center;
  vertical-align: top;
  cursor: pointer;
}
.rec-media {
  width: 240px;
}
.rec-profile {
  width: 200px;
  display: inline-block;
  color: #444;
}
.rec-price {
  text-decoration: line-through;
}
.rec-online-price {
  color: #ff0036;
  font-size: 16px;
}
.rec-params {
  font-size: 12px;
  color: #888;
}
.gs-link {
  color: #999;
  text-decoration: none;
  outline: none;
}
.gs-forbid {
  cursor: not-allowed;
}
.gs-menu-bg {
  position: absolute;
  width: 100%;
  height: 30px;
  background-color: #f2f2f2;
  border-bottom: 1px solid #e5e5e5;
}
.gs-header {
  width: 1120px;
  margin-left: auto;
  margin-right: auto;
}
.gs-quick-menu {
  position: relative;
  font-size: 12px;
  color: #999;
  background-color: #f2f2f2;
}
.gs-profile {
  display: inline-block;
  line-height: 30px;
  cursor: pointer;
}
.gs-nav {
  position: absolute;
  right: 0;
  display: inline-block;
  line-height: 30px;
  list-style: none;
}
.gs-nav-item {
  margin-left: 12px;
  display: inline-block;
}
.gs-logo {
  display: inline-block;
  margin-top: 10px;
  margin-bottom: 10px;
  width: 188px;
  height: 75px;
  cursor: pointer;
  background-image: url("/logo.png");
  background-repeat: no-repeat;
  background-size: cover;
}
.gs-search-box {
  display: inline-block;
  line-height: 100px;
  float: right;
}
.gs-search-input {
  box-sizing: border-box;
  width: 240px;
  line-height: 32px;
  padding-left: 6px;
  outline: none;
  border: 2px solid #95bf47;
  vertical-align: middle;
}
.gs-search-btn {
  display: inline-block;
  line-height: 36px;
  padding-left: 16px;
  padding-right: 16px;
  color: #fff;
  font-weight: 600;
  background-color: #95bf47;
  vertical-align: middle;
  cursor: pointer;
  user-select: none;
}
.gs-dividor {
  height: 2px;
  background-color: #95bf47;
}
</style>
