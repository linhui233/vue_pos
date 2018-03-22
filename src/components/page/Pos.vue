<template>
  <div class="pos">
    <div>
        <el-row>
            <el-col :span="7" class="pos-order" id="order-list">
                <el-tabs type="card">
                    <el-tab-pane label="点餐" >
                        <el-table :data="tableData" broder show-summary style="width:100%">
                            <el-table-column prop="goodsName" label="商品"></el-table-column>
                            <el-table-column prop="count" label="数量" width="60"></el-table-column>
                            <el-table-column prop="price" label="金额" width="70"></el-table-column>
                            <el-table-column label="操作" width="100" fixed="right">
                                <template scope="scope">
                                    <el-button type="text" size="small">删除</el-button>
                                    <el-button type="text" size="small">增加</el-button>
                                </template>
                            </el-table-column>
                        </el-table>
                        <div class="button">
                            <el-button type="warning">下单</el-button>
                            <el-button type="danger">删除</el-button>
                            <el-button type="success">结账</el-button>
                        </div>
                    </el-tab-pane>
                    <el-tab-pane label="挂单">
    
                    </el-tab-pane>
                    <el-tab-pane label="外卖">
    
                    </el-tab-pane>
                </el-tabs>
               
            </el-col>
            <el-col :span="17">
                <div>
                    <div class="title">常用商品</div>
                    <div class="popular-goods">
                        <ul>
                            <li v-for="goods in popularGoods">
                                <span>{{goods.goodsName}}</span>
                                <span>{{goods.price}}</span>
                            </li>
                        </ul>
                    </div>
                </div>
                <div class="goods-type">
                    <el-tabs>
                        <el-tab-pane label="汉堡">
                            <ul class="goods-type-list">
                                <li v-for="good in typeGoods.type0">
                                    <span class="foodImg"><img :src="good.goodsImg" width="100%"></span>
                                    <span class="foodName">{{good.goodsName}}</span>
                                    <sapn class="foodPrice">￥{{good.price}}</sapn>
                                </li>
                            </ul>
                        </el-tab-pane>
                        <el-tab-pane label="小吃">小吃</el-tab-pane>
                        <el-tab-pane label="饮料">饮料</el-tab-pane>
                        <el-tab-pane label="套餐">套餐</el-tab-pane>
                    </el-tabs>
                </div>
            </el-col>
        </el-row>
    </div>
  </div>
</template>

<script>
    export default {
        name: "pos",
        data(){
            return {
                tableData: [{
                    goodsName: "可口可乐",
                    price: 3,
                    count: 1
                },{
                    goodsName: "香辣鸡腿堡",
                    price: 16,
                    count: 1
                },{
                    goodsName: "薯条",
                    price: 8,
                    count: 1
                },{
                    goodsName: "甜筒",
                    price: 4,
                    count: 1
                }],
                popularGoods:[
                {
                    goodsId:1,
                    goodsName:'香辣鸡腿堡',
                    price:18
                }, {
                    goodsId:2,
                    goodsName:'田园鸡腿堡',
                    price:15
                }, {
                    goodsId:3,
                    goodsName:'和风汉堡',
                    price:15
                }, {
                    goodsId:4,
                    goodsName:'快乐全家桶',
                    price:80
                }, {
                    goodsId:5,
                    goodsName:'脆皮炸鸡腿',
                    price:10
                }, {
                    goodsId:6,
                    goodsName:'魔法鸡块',
                    price:20
                }, {
                    goodsId:7,
                    goodsName:'可乐大杯',
                    price:10
                }, {
                    goodsId:8,
                    goodsName:'雪顶咖啡',
                    price:18
                }, {
                    goodsId:9,
                    goodsName:'大块鸡米花',
                    price:15
                }, {
                    goodsId:20,
                    goodsName:'香脆鸡柳',
                    price:17
                }],
                typeGoods: {
                    type0: [{
                        goodsId: 1,
                        goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
                        goodsName: "香辣鸡腿堡",
                        price: 18
                    }, {
                        goodsId:2,
                        goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
                        goodsName:'田园鸡腿堡',
                        price:15
                    }, {
                        goodsId:3,
                        goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
                        goodsName:'和风汉堡',
                        price:15
                    }],
                    type1Goods: [{
                    
                    }]
                }
            }
        },
        mounted:function(){
            var orderHeight = document.body.clientHeight;
            console.log(orderHeight);
            document.getElementById("order-list").style.height = orderHeight+'px';
        },
        methods:{
            //商品是否已经存在于订单列表中
            //根据判断的值编写业务逻辑
        }
        
    }
</script>

<style scoped>
.pos-order{
    background-color: #F9FAFC;
    border-right: 1px solid #C0CCDA;
    height:100%;
}
.button{
    margin-top: 10px;
    text-align: center;
}
.title{
    height: 18px;
    border-bottom: 1px solid #D3dce6;
    background-color: #F9FAFC;
    padding: 10px;
}
.popular-goods ul li{
    list-style: none;
    float: left;
    border: 1px solid #E5E9F2;
    padding: 10px;
    margin: 5px;
    background-color: #fff;
}
.goods-type{
    clear: both;
}
.goods-type-list li{
    list-style: none;
    width: 23%;
    border: 1px solid #E5E9F2;
    height: auto;
    overflow: hidden;
    background-color: #fff;
    padding: 2px;
    float: left;
    margin: 2px;
}
.goods-type-list li span {
    display: block;
}
.foodImg{
    width: 40%;
    float:left;
}
.foodName{
    font-size: 18px;
    padding-left: 10px;
    color:brown;
    
}
.foodPrice{
    font-size: 16px;
    padding-left: 10px;
    padding-top: 10px;
    text-align: center;
}
</style>
