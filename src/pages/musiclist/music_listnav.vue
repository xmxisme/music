<template>
  <div class="music-nav">
    <div class="log url hd">
      <h2>云音乐特色榜</h2>
      <div class="more">更多</div>
    </div>
    <ul>
      <li>
        <router-link to="/home/hot" :class="this.$route.path == '/home/hot' ?'active':''">飙升榜</router-link>
        <span class="gap-line"> </span>
      </li>
      <li>
        <router-link to="/home/news" :class="this.$route.path == '/home/news' ?'active':''">新歌榜</router-link>
        <span class="gap-line"> </span>
      </li>
      <li>
        <router-link to="/home/king" :class="this.$route.path == '/home/king' ?'active':''">原创榜</router-link>
        <span class="gap-line"> </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default{

}
</script>

<style scoped>

.music-nav{
  background-color: #fff;
  margin-top: 10px;
  padding: 10px 17px;
}

.hd{
  margin: 14px 0 18px 0;
  display: -webkit-box;
  display: -webkit-flex;
  display: flex;
}

.hd h2{
  -webkit-box-flex: 1;
  -webkit-flex: 1;
  flex: 1;
  margin: 0;
  padding: 0;
  font-size: 20px;
}

.hd div{
  width: 64px;
  font-size: 12px;
  text-align: right;
}

.hd{
  margin-bottom: 0;
}

ul{
  display: flex;
}

ul li{
  padding: 18px 0 12px 0;
  font-size: 16px;
  flex: 1;
  text-align: center;
  color: #999;
  position: relative;
  z-index: 2;
}

ul li a{
  color: #000;
  display: block;
}

ul li a:hover{
  color: #299DE7 !important;
}

ul li a:active{
  color: #299DE7 !important;
}
.gap-line{
  position: absolute;
  right: 0;
  top: 20px;
  height: 18px;
  width: 1px;
  border-left: 1px solid #eee;
}

.active{
  color: #299DE7
}

.more:hover{
  text-decoration: underline;
  cursor: pointer;
}
</style>