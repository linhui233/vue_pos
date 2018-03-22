<template>
  <div class="pos">
    <div>
        <el-row>
            <el-col :span="10" class="pos-order" id="order-list">
                <el-tabs type="card">
                    <el-tab-pane label="点餐" >
                        <el-table :data="tableData" broder style="width:100%">
                            <el-table-column prop="goodsName" label="商品"></el-table-column>
                            <el-table-column prop="count" label="数量" width="60"></el-table-column>
                            <el-table-column prop="price" label="金额" width="70"></el-table-column>
                            <el-table-column label="操作" width="100" fixed="right">
                                <template scope="scope" >
                                    <el-button type="text" size="small" @click="delFromOrder(scope.row)">删除</el-button>
                                    <el-button type="text" size="small" @click="addToOrder(scope.row)">增加</el-button>
                                    <!--作用域插槽scope-->
                                </template>
                            </el-table-column>
                        </el-table>
                        <div class="totalDiv">
                            <span class="totalDiv-sum">总数量:{{totalAmount}}</span>
                            <span>总金额:{{totalPrice}}</span>
                        </div>
                        <div class="button">
                            <el-button type="warning" @click="order()">下单</el-button>
                            <el-button type="danger" @click="delAllGoods()">删除</el-button>
                            <el-button type="success" @click="pay()">结账</el-button>
                        </div>
                    </el-tab-pane>
                    <el-tab-pane label="订单">
                        订单
                    </el-tab-pane>
                    <el-tab-pane label="外卖">
                        外卖
                    </el-tab-pane>
                </el-tabs>
               
            </el-col>
            <el-col :span="14">
                <div>
                    <div class="title">常用商品</div>
                    <div class="popular-goods">
                        <ul>
                            <li v-for="goods in popularGoods" @click="addToOrder(goods)">
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
                                <li v-for="goods in typeGoods.type0" @click="addToOrder(goods)">
                                    <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                                    <span class="foodName">{{goods.goodsName}}</span>
                                    <span class="foodPrice">￥{{goods.price}}</span>
                                </li>
                            </ul>
                        </el-tab-pane>
                        <el-tab-pane label="小吃">
                            <ul class="goods-type-list">
                                <li v-for="goods in typeGoods.type1" @click="addToOrder(goods)">
                                    <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                                    <span class="foodName">{{goods.goodsName}}</span>
                                    <span class="foodPrice">￥{{goods.price}}</span>
                                </li>
                            </ul>
                        </el-tab-pane>
                        <el-tab-pane label="饮料">
                            <ul class="goods-type-list">
                                <li v-for="goods in typeGoods.type2" @click="addToOrder(goods)">
                                    <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                                    <span class="foodName">{{goods.goodsName}}</span>
                                    <span class="foodPrice">￥{{goods.price}}</span>
                                </li>
                            </ul>
                        </el-tab-pane>
                        <el-tab-pane label="套餐">
                            <ul class="goods-type-list">
                                <li v-for="goods in typeGoods.type3" @click="addToOrder">
                                    <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                                    <span class="foodName">{{goods.goodsName}}</span>
                                    <span class="foodPrice">￥{{goods.price}}</span>
                                </li>
                            </ul>
                        </el-tab-pane>
                    </el-tabs>
                </div>
            </el-col>
        </el-row>
    </div>
  </div>
</template>

<script>
    import axios from 'axios'
    export default {
        name: "pos",
        data(){
            return {
                tableData: [],
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
                    type0: [],
                    type1: [],
                    type2: [],
                    type3: [],
                },
                totalAmount: 0,
                totalPrice: 0
            }
        },
        created:function(){
          //这里使用了axios,一种基于promise的HTTP库.
          axios.get('http://jspang.com/DemoApi/typeGoods.php')
            .then(response=>{
                console.log(response);
                this.typeGoods.type0 = response.data[0];
                this.typeGoods.type1 = response.data[1];
                this.typeGoods.type2 = response.data[2];
                this.typeGoods.type3 = response.data[3];
                //es6语法
                //xxx=>{} 等价于 function(xxx){};
                
            })
            .catch(error=>{
              alert("网络错误，读取数据失败");
            })
        },
        mounted:function(){
            var orderHeight = document.body.clientHeight;
            console.log(orderHeight);
            document.getElementById("order-list").style.height = orderHeight+'px';
        },
        methods:{
            //添加到订单列表的方法
            addToOrder(goods){
                this.totalAmount = 0;
                this.totalPrice = 0;
                let isHave = false;
                //判断点击的商品是否已经在订单列表中
                for(let i=0;i<this.tableData.length;i++){
                    if(this.tableData[i].goodsId == goods.goodsId){
                        isHave = true;
                    }
                }
                if(isHave){
                    let arr = this.tableData.filter(o => o.goodsId == goods.goodsId);
                    //此处=>后不能加入 {}
                    console.log(arr);
                    arr[0].count++;
                }else{
                    let newGoods = {
                        goodsId:goods.goodsId,
                        goodsName:goods.goodsName,
                        price:goods.price,
                        count:1
                    }
                    console.log(newGoods);
                    this.tableData.push(newGoods);
                }
                //重新计算数量和金额
                this.reCalculateMoney();
            },
            delFromOrder(goods){
                this.tableData = this.tableData.filter(o=>o.goodsId!=goods.goodsId);
                this.reCalculateMoney();
            },
            reCalculateMoney(){
                this.totalAmount = 0;
                this.totalPrice = 0;
                if(this.tableData){
                    this.tableData.forEach(element=>{
                        this.totalAmount += element.count;
                        this.totalPrice = this.totalPrice+(element.price*element.count);
                    })
                }
            },
            delAllGoods(){
                this.tableData = [];
                this.totalAmount = 0;
                this.totalPrice = 0;
            },
            pay(){
                if(this.tableData.length !== 0){
                    this.tableData = [];
                    this.totalAmount = 0;
                    this.totalPrice = 0;
                    this.$message({
                        message: '支付成功，正在急速制作中!',
                        type: 'success'
                    });
                }else{
                    this.$message.error('请先订购些商品吧');
                }
            },
            order(){
                if(this.totalAmount != 0){
                    this.tableData = [];
                    this.totalAmount = 0;
                    this.totalPrice = 0;
                    this.$message({
                        message: '下单成功，请到订单页面付款,或者你可以再逛逛',
                        type: 'success'
                    });
                }else{
                    this.$message.error('请先订购些商品吧');
                }
            }
            
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
    height: 20px;
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
    cursor: pointer;
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
    cursor: pointer;
}
.goods-type-list li span {
    display: block;
}
.foodImg{
    width: 40%;
    float:left;
}
.foodName{
    font-size: 1vw;
    padding-left: 10px;
    color:brown;
    
}
.foodPrice{
    font-size: 2vw;
    padding-left: 10px;
    padding-top: 10px;
    text-align: center;
}
.totalDiv-sum{
    margin-right: 15px;
}
</style>
