<template>
    <div class="goods-list">
<!--        <router-link  to="'/home/goodsinfo/' + item.id"   tag="div" class="goods-item" v-for="item in goodslist" :key="item.id">-->
<!--            <img :src="item.img_url" alt="">-->
<!--            <h1 class="title">{{ item.title }}</h1>-->
<!--            <div class="info">-->
<!--                <p class="price">-->
<!--                    <span class="now">￥{{ item.sell_price }}</span>-->
<!--                    <span class="old">￥{{ item.market_price }}</span>-->
<!--                </p>-->
<!--                <p class="sell">-->
<!--                    <span>热卖中</span>-->
<!--                    <span>剩{{ item.stock_quantity }}件</span>-->
<!--                </p>-->
<!--            </div>-->
<!--        </router-link>-->

<!--在网页中，有2种跳转方式:
    1,以a标签的方式跳转.叫标签跳转，上面的router就是a标签的跳转形式
    2.以代码的形式跳转，使用window。location.href 的形式，叫做编程式导航,vue-router中有介绍 也就是用JS代码进行编程
      通过给上面绑定个点击事件，然后定义事件，能达到同样的效果，-->


        <div  class="goods-item" v-for="item in goodslist" :key="item.id" @click="goodetail(item.id)">
            <img :src="item.img_url" alt="">
            <h1 class="title">{{ item.title }}</h1>
            <div class="info">
                <p class="price">
                    <span class="now">￥{{ item.sell_price }}</span>
                    <span class="old">￥{{ item.market_price }}</span>
                </p>
                <p class="sell">
                    <span>热卖中</span>
                    <span>剩{{ item.stock_quantity }}件</span>
                </p>
            </div>
        </div>

        <mt-button type="danger" size="large" @click="getMore">加载更多</mt-button>
    </div>

</template>

<script>
    export  default{
        data(){//data是往自己组件内部，挂载一些私有数据的
            return{
                pageindex:1 ,//分页的页数
                goodslist:[]//存放商品列表的数组
            }
        },
        created(){
            this.getGoodsList();
        },
        methods:{
            getGoodsList(){
                this.$http.get('api/getgoods?pageindex=' + this.pageindex ).then(result =>{
                    if(result.body.status === 0){
                        this.goodslist = this.goodslist.concat( result.body.message)  ;
                    }
                })
            },
            getMore(){
                this.pageindex++;
                this.getGoodsList()
            },
            goodetail(id){
            //    使用js的形式进行路有导航
            //    注意：一定要区分 this.$route 和 this.$touter 这2个对象
            //    注意：this.$route 是路由【参数对象】，所有路由中的参数，params。query 都属于他
            //    注意：this.$router 是一个路由【导航对象，用它可以方便的使用JS代码，实现
                //    路由的前进，后退，跳转到新的URL地址】
                // console.log(this); 可以查看所有router属性
                //第一种，最简单的方式
                this.$router.push("/home/goodsinfo/" + id);

                //主要有4种引入方式：
                // 字符串
                // router.push('/home/goodsinfo/')

                // 对象
                // router.push({ path: '/home/goodsinfo/' })

                // 命名的路由
                // router.push({ name: 'goodsinfo', params: { userId: 'id' }})

                // 带查询参数，变成 /register?plan=private
                // router.push({ path: 'register', query: { plan: 'private' }})
            }
        }
    }

</script>

<style scoped>
    .goods-list{
        display: flex;
        flex-wrap: wrap;
        padding: 7px;
        justify-content: space-between;
    }
    .goods-list .goods-item{
        width: 49%;
        border: 1px solid #ccc;
        box-shadow: 0 0 8px #ccc;
        margin: 4px 0;
        padding: 2px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        min-height: 293px;
    }
    .goods-list .goods-item img{
        width: 100%;
    }
    .title{
        font-size: 14px;
    }

    .info{
        background-color: #eee;}
    .info  p{
        margin: 0;
        padding: 5px;
    }
    .price .now{
        color: red;
        font-weight: bold;
        font-size: 16px;
    }
    .price  .old{
        text-decoration: line-through;
        font-size: 12px;
        margin-left: 10px;
    }
    .price .sell{
        display: flex;
        justify-content: space-between;
        font-size: 13px;
    }
</style>