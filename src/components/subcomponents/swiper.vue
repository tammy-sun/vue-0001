<template>
    <div>
        <mt-swipe :auto="4000">
            <!-- 在组件中，使用v-for循环的话，一定要使用 key -->
<!--            将来，谁使用此轮播图软件，谁为我们传递lunbotulist-->
<!--            此时，lunbotulist 应该是，父组件向子组件传值，来设置-->
            <mt-swipe-item v-for="item in lunbotuList" :key="item.url">
                <img :src="item.img" alt=""  :class="{full: isfull}">
            </mt-swipe-item>
        </mt-swipe>
    </div>
</template>
<!-- 分析：为什么 商品评论中的 轮播图那么丑： -->
<!-- 1. 首页中的图片，它的宽和高，都是 使用了 100% 的宽度 -->
<!-- 2. 在商品详情页面中，轮播图的 图片，如果也使用 宽高 为 100%的话，页面不好看 -->
<!-- 3. 商品详情页面中的轮播图，期望 高度是 100%， 但是 宽度为 自适应 -->
<!-- 4. 经过分析，得到 问题的原因： 首页中的轮播图 和 详情中的轮播图，分歧点是 宽度到底是 100% 还是 自适应 -->
<!-- 5. 既然这两个 轮播图，其它方面都是没有冲突的，只是 宽度有分歧， 那么，我们可以定义一个 属性，让 使用轮播图的 调用者，手动指定 是否为 100% 的宽度 -->

<script>
    export default {
        props:["lunbotulist","isfull"]
    }
</script>

<style scoped>
    .mt-swipe {
        height: 200px;
        /*  引入的轮播图，默认是没有高度的，要后期去设置*/
    }
    .mint-swipe .mint-swipe-item{
        text-align: center;
    }
    /*.mint-swipe .mint-swipe-item:nth-child(1) {*/
    /*    background-color: red;*/
    /*}*/
    /*.mint-swipe .mint-swipe-item:nth-child(2) {*/
    /*    background-color: blue;*/
    /*}*/
    /*.mint-swipe .mint-swipe-item:nth-child(3) {*/
    /*    background-color: cyan;*/
    /*}*/
    .mint-swipe   img {
        /*width: 100%;*/
        height: 100%;
    }
    .full{
        width:100%
    }
</style>