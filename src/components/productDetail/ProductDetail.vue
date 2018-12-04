<template>
  <transition name="food-detail">
    <div class="food" v-show="showFlag">
      <div class="food-wrapper">
        <div class="food-content">
          <div class="img-wrapper">
            <img :src="food.picture" class="food-img"  />
            <span
              class="close-bt icon-close"
              @click="closeView"
            ></span>
            <img class="share-bt" src="./img/share.png" />
            <img class="more-bt" src="./img/more.png" />
          </div>
          <div class="content-wrapper">
            <h3 class="name">{{food.name}}</h3>
            <p class="saled">{{food.month_saled_content}}</p>
            <img class="product" v-show="food.product_label_picture" :src="food.product_label_picture"/>
            <p class="price">
              <span class="text">￥{{food.min_price}}</span>
              <span class="unit">/{{food.unit}}</span>
            </p>

            <div class="cartcontrol-wrapper">
              <app-cartcontrol :food="food"></app-cartcontrol>
            </div>
            <div
              class="buy"
              @click="addProduct"
              v-show="!food.count || food.count == 0">
              选规格
            </div>
          </div>
        </div>
      </div>
    </div>
  </transition>

</template>

<script>
  import Vue from 'vue'
  import Cartcontrol from '../cartcontrol/Cartcontrol'
  export default {
    data(){
      return {
        showFlag:false
      }
    },
    props:{
      food:{
        type:Object
      }
    },
    methods:{
      showView(){
        this.showFlag = true
      },
      closeView(){
        this.showFlag = false
      },
      addProduct(){
        Vue.set(this.food,'count',1)
      }
    },
    components:{
      'app-cartcontrol':Cartcontrol
    }
  }
</script>

<style scoped>
  @import url(../../common/css/icon.css);
  .food{
    position:fixed;
    left:0;
    top:0;
    bottom:51px;
    background:white;
    width:100%;
    z-index:90;
  }

  /*动画*/
  .food-detail-enter-active, .food-detail-leave-active {
    transition:  1.0s
  }
  .food-detail-enter, .food-detail-leave-to {
    transform: translateX(100%);
  }

  .food .food-wrapper .food-content{
    width:100%;
  }
  /*为了实现把图片的位置预留出来*/
  .food .food-wrapper .food-content .img-wrapper{
    position: relative;
    width: 100%;
    height: 0;
    padding-top: 100%;
  }

  /*图片样式*/
  .food .food-wrapper .food-content .img-wrapper .food-img{
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 100%;
  }
  .food .food-wrapper .food-content .img-wrapper .close-bt{
    width: 30px;
    height: 30px;
    position: absolute;
    left: 10px;
    top: 10px;
    text-align: center;
    font-size: 30px;
    color: white;
    background: #7f7f7f;
    border-radius: 50%;
  }
  .food .food-wrapper .food-content .img-wrapper .share-bt,
  .food .food-wrapper .food-content .img-wrapper .more-bt
  {
    width: 30px;
    height: 30px;
    position: absolute;
    top: 10px;
  }
  .food .food-wrapper .food-content .img-wrapper .share-bt{
    right: 50px;
  }
  .food .food-wrapper .food-content .img-wrapper .more-bt{
    right: 10px;
  }

  .food .food-wrapper .food-content .content-wrapper{
    padding: 0 0 16px 16px;
    position: relative;
  }
  .food .food-wrapper .food-content .content-wrapper .name{
    font-size: 15px;
    color: #333333;
    line-height: 30px;
    font-weight: bold;
  }
  .food .food-wrapper .food-content .content-wrapper .saled{
    font-size: 11px;
    color: #9d9d9d;
    margin-bottom: 6px;
  }
  .food .food-wrapper .food-content .content-wrapper .product{
    height: 15px;
    margin-bottom: 16px;
  }
  .food .food-wrapper .food-content .content-wrapper .price{
    font-size: 0;
  }
  .food .food-wrapper .food-content .content-wrapper .price .text{
    font-size: 17px;
    color: #FB4E44;
  }
  .food .food-wrapper .food-content .content-wrapper .price .unit{
    font-size: 11px;
    color: #9D9D9D;
  }
  .food .food-wrapper .food-content .cartcontrol-wrapper{
    position: absolute;
    right: 12px;
    bottom: 10px;
    padding: 2px;
  }
  .food .food-wrapper .food-content .buy{
    width: 64px;
    height: 30px;
    font-size: 12px;
    line-height: 30px;
    text-align: center;
    background: #FFD161;
    border-radius: 30px;
    position: absolute;
    right: 12px;
    bottom: 10px;
  }
</style>
