<template>
    <div class="cartcontrol">
        <transition name="decrease">
            <div class="cart-decrease" v-show="food.count>0" @click.stop.prevent="decreaseCart">
                <span class="inner icon-remove_circle_outline"></span>
            </div>
        </transition>
        <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
        <div class="cart-add icon-add_circle" @click.stop.prevent="addCart"></div>
    </div>
</template>

<script>
    import BScroll from 'better-scroll';
    import shopcart from '../shopcart/shopcart.vue';
    import cartcontrol from '../cartcontrol/cartcontrol.vue'
    import Vue from 'vue'

    export default {
        props: {
            food: {
                type: Object
            }
        },
        methods: {
            addCart(event) {
                // 防止用户多次点击
                if (!event._constructed) {
                    return;
                }
                if(!this.food.count) {
                    Vue.set(this.food, 'count', 1);
                    // this.food.count = 1;
                } else {
                    this.food.count++;
                }
                this.$emit('cart-add', event.target);
            },
            decreaseCart(s) {
                if (!event._constructed) {
                    return;
                }
                if(this.food.count) {
                    this.food.count--;
                }
            }
        }
    };
</script>
<style lang="stylus" rel="stylesheet/stylus">
    .cartcontrol
        font-size 0
        .cart-decrease
            display inline-block
            padding 6px
            transition all 0.4s linear
            opacity 1
            transform translate3d(0, 0, 0)
            &.decrease-enter,&.decrease-leave-to
                transform translate3D(24px, 0, 0)
                opacity: 0;
                .inner
                    transform rotate(180deg)
            .inner
                display inline-block
                line-height 24px
                font-size 24px
                color rgb(0, 160, 220)
                transition all 0.4s linear
                transform rotate(0) 
        .cart-decrease
            display inline-block
        .cart-count
            display inline-block
            vertical-align top
            width 12px
            padding-top 6px
            line-height 24px
            text-align center 
            font-size 10px
            color rgb(147, 153, 159)
        .cart-add
            display inline-block
            padding 6px
            line-height 24px
            font-size 24px
            color rgb(0, 160, 220)
</style>