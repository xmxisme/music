<template>
  <el-carousel indicator-position="outside">
    <el-carousel-item v-for="(item,index) in rotationChart.slice(0,8)" :key="index">
      <img :src="item.pic" alt="">
    </el-carousel-item>
  </el-carousel>
</template>

<style>
  .el-carousel__container{
    height: 140px !important;
    margin-top: 10px;
  }
  .el-carousel-item{
    background-color: #fff;
  }
  .el-carousel__item img {
    width: 95%;
    color: #fff;
    margin: 0;
    padding: 10px 2.5% 0 2.5%;
  }
  .el-carousel__indicators--outside{
    background-color: #fff;
  }

 .el-carousel__item:nth-child(2n) {
    background-color: #fff;
  }

  .el-carousel__item:nth-child(2n+1) {
    background-color: #fff;
  }
</style>

<script>
export default{
  name: 'rotationChart',
  data(){
    return{
      rotationChart:[]
    }
  },
  mounted(){
    // 轮播图
    var url = this.HOST  + "/banner/?type=2"
    this.$axios.get(url)
    .then(res => {
      this.rotationChart = res.data.banners

    })
    .catch(erro => {
      console.log(erro)
    })
  }
}
</script>
