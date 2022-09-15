<!-- 推荐歌单: 热歌榜/美国Billboard排行榜 -->
<template lang="html">
  <div class="mod-albums">
    <div class="hd log url">
      <h2>{{title}}</h2>
      <div>
        <router-link class="more" :to="{ name: 'MoreList', params:{musicid:this.musicid,musictitle:title}}" tag="div" >更多</router-link>
      </div>

    </div>

    <div class="container">
      <div class="gallery">
         <div class="scroller">
           <router-link tag="div" :to="{name:'MusicPlay',params:{songid:item.id,songname:item.name,songar:item.ar}}" class="card url" v-for="(item,index) in todayRecommend" :key="index">
              <div class="album">
                <img :src="item.al.picUrl"/>
                <div class="name more">{{item.name}}</div>
              </div>
           </router-link>
         </div>
       </div>
    </div>
  </div>
</template>

<script>
export default{
  name: 'todayRecommend',
  data(){
    return{
      todayRecommend:[]
    }
  },
  props:{
    title:{
      type:String,
      default:"热歌榜"
    },
    musicid:{
      type:String,
      default:"0 ",
    }
  },
  
  mounted(){
    // 热歌榜 取前6
    var httpurl = this.HOST  + "/playlist/track/all?id="+ this.musicid +"&limit=6"
    this.$axios.get(httpurl)
    .then(res => {
      this.todayRecommend = res.data.songs
    })
    .catch(erro => {
      console.log(erro)
    })
  }
}
</script>

<style scoped>

.mod-albums{
  background-color: #fff;
  padding: 10px 17px;
}

.more:hover{
  text-decoration: underline;
  cursor: pointer;
}

.hd{
  display: flex;
  margin: 14px 0 18px 0;
}
.hd h2{
  -webkit-box-flex: 1;
  -webkit-flex:1;
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

.mod-albums .gallery{
  overflow: hidden;
  margin: 0 -5px;
}

.mod-albums .gallery .card{
  width: 33.3%;
  float: left;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  padding: 0 5px 10px;
}

.mod-albums .gallery .card .album{
  position: relative;
}

.mod-albums .gallery .card img{
  width: 100%;
  height: auto;
  border: 1px solid #eee;
}

.mod-albums .gallery .card .name{
  font-size: 12px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  margin-top: 4px;
  line-height: 14px;
  max-height: 28px;
  margin-bottom: 2px;
}

</style>
