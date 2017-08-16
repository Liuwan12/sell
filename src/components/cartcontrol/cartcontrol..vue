<template>
<div class="cartcontrol">
  <transition name="fade">
    <div class="cart-decrease icon-remove_circle_outline" v-show="food.count>0"
         @click.stop.prevent="decreaseCart" transition="move">
    </div>
  </transition>
  <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
  <div class="cart-add icon-add_circle" @click.stop.prevent="addCart($event)"></div>
</div>
</template>

<script type="text/ecmaScript-6">
  import Vue from 'vue';
 export default {
     props: {
         food: {
             type: Object
         }
     },
   methods: {
       addCart (event) {
         if (!event._constructed) {
           return;
         }
         if (!this.food.count) {
           Vue.set(this.food, 'count', 1);
           this.food.count = 1;
         } else {
           this.food.count++;
         }
         this.$emit('increment', event.target);
         // 子组件通过 $emit触发父组件的方法
       },
     decreaseCart (event) {
       if (!event._constructed) {
         return;
       }
       if (this.food.count) {
         this.food.count--;
       }
     }
   }
 };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"
  .cartcontrol
     font-size 0
     .icon-remove_circle_outline,.icon-add_circle
         font-size 24px
         line-height 24px
         display inline-block
         padding 6px
         color rgb(0,160,220);
     .cart-count
         display inline-block
         font-size 10px
         vertical-align top
         width: 12px
         padding-top 6px
         line-height 24px
         text-align center
         color rgb(147,153,159)
      .icon-add_circle
         display inline-block
</style>
