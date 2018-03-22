<template>
  <div class="left-nav">
    <ul>
      <li>
        <i class="iconfont icon-shouye"></i>
        <div>首页</div>
      </li>
      <li>
        <i class="iconfont icon-wodedingdan"></i>
        <div>店铺</div>
      </li>
      <li>
        <i class="iconfont icon-gouwuche"></i>
        <div>商品</div>
      </li>
      <li>
        <i class="iconfont icon-xiaoxizhongxin"></i>
        <div>消息</div>
      </li>
    </ul>
  </div>
</template>

<script>
    export default {
        name: "left-nav"
    }
</script>

<style>
  .left-nav {
    height: 100%;
    color: #fff;
    float: left;
    width: 5%;
    background-color: #1D8ce0;
  }
  .left-nav ul{
    padding: 0px;
    margin: 0px;
  }
  .left-nav li i {
    font-size: 20px;
  }
  .left-nav li{
    font-size: 16px;
    font-family: "微软雅黑";
    list-style: none;
    text-align: center;
    border-bottom: 1px solid #20a0ff;
    padding: 15px 0px 15px 0;
  }
</style>
