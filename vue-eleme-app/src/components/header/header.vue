<template>
    <div class="header">
        <div class="content-wrapper">
            <div class="avatar">
                <img width="64" height="64"
                 :src="seller.avatar">
            </div>
            <div class="content">
                <div class="title">
                    <span class="brand">
                    </span>
                    <span class="name">{{seller.name}}</span>
                </div>
                <div class="description">
                    {{seller.description}}/
                    {{seller.deliveryTime}}分钟送达
                </div>
                <div class="support"
                 v-if="seller.supports">
                    <span class="icon" 
                    :class="classMap[seller.supports[0].type]">
                    </span>
                    <span class="text">
                        {{seller.supports[0].description}}
                    </span>
                </div>
            </div>
            <div class="support-count"
                v-if="seller.supports"  @click="showDetail">
                <span class="count">{{seller.supports.length}}</span>
                <i class="icon-keyboard_arrow_right"></i>
            </div>
        </div>
        <transition name="fade">
            <div v-show="detailShow" class="detail">
               <div class="detail-wrapper clearfix">
                   <div class="detail-main">
                       <h1 class="name">{{seller.name}}</h1>
                       <div class="star-wrapper">
                           <star :size="48" :score="seller.score"></star>      
                       </div>
                   </div>
               </div>
            </div>
        </transition>  
    </div>
</template>
<script>
    import star from '@/components/star/star'
    export default {
        // 向外声明参数 同时，要求类型
        props: {
            seller: {
                type: Object
            }
        },
        data () {
            return {
                // 子组件内的数据项一般主要是用于
                // 组件内状态的切换，不涉及数据的交换
                detailShow: false
            }
        },
        methods: {
            showDetail () {
                this.detailShow = true
            }
        },
        created () {
            this.classMap = ['decrease', 'discount',
            'special', 'invoice', 'guarantee']
        },
        components:{
            star
        }
    }
</script>
<style lang="stylus" rel="stylesheet/stylus">
    @import '../../common/stylus/mixin.styl'

    .header
        position relative
        overflow hidden
        color #ffffff
        background rgba(7, 17, 27, 0.5)
        .content-wrapper
            position relative
            padding 24px 12px 18px 24px
            font-size 0
            .avatar
                display inline-block
                vertical-align top
                img
                    border-radius 2px
            .content
                display inline-block
                margin-left 16px
                .title
                    margin 2px 0 8px 0
                    .brand
                        display inline-block
                        vertical-align top
                        width 30px
                        height 18px
                        bg-image('brand')
                        background-size 30px 18px
                        background-repeat no-repeat
                    .name
                        margin-left 6px
                        font-size 16px
                        line-height 18px
                        font-weight bold
                
                .description
                    margin-bottom 10px
                    line-height 12px
                    font-size 12px
                .support
                    .icon
                        display inline-block
                        vertical-align top
                        width 12px
                        height 12px
                        margin-right 4px
                        background-size 12px 12px
                        background-repeat no-repeat
                        &.decrease
                            bg-image('decrease_1')
                        &.discount
                            bg-image('discount_1')
                        &.guarantee
                            bg-image('guarantee_1')
                        &.invoice
                            bg-image('invoice_1')
                        &.special
                            bg-image('special_1')
            
            .support-count
                position absolute
                right 12px
                bottom 14px
                padding 0 8px
                height 24px
                line-height 24px
                border-radius 14px
                background rgba(0,0,0,.2)
                text-align center
                .count
                    vertical-align center
                    font-size 10px
                .icon-keyboard_arrow_right
                    margin-left 2px
                    line-height 24px
                    font-size 10px
        .detail
            position fixed
            z-index 100
            top 0
            left 0
            width 100%
            height 100%
            overflow auto
            opacity 1
            background rgba(7,17,27,0.8)
            &.fade-enter-active, &.fade-leave-active
                transition all .5s
            &.fade-enter, &.fade-leave
                opacity 0
                background rgba(7, 17, 27, 0)

</style>