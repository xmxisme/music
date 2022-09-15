<template lang="html">
  <div class="artists">
    <ul class="list">
      <router-link tag="li" :to="{name:'ArtistsDetails',params:{avatar:item.img1v1Url,name:item.name,tingid:item.id}}" :key="index" class="artist" v-for="(item,index) in artistsArr">
        <div class="pic">
          <img :alt="item.name" :src="item.img1v1Url">
        </div>

        <div class="info">
          <div>{{item.name}}</div>
        </div>
      </router-link>
    </ul>
  </div>
</template>

<script>
//https://music.cyrilstudio.top/artist/list?type=-1&area=7 华语歌手
export default{
  name:"artists",
  data(){
    return{
      // 歌手信息
      artistsArr:[
        {
          name:"",
          img1v1Url:""
        }
      ]
    }
  },
  mounted(){
    // 获取华语歌手前30
    var idUrl = this.HOST  + "/artist/list?type=-1&area=7"
    this.$axios.get(idUrl)
    .then(res => {
    this.artistsArr = res.data.artists
    // console.log(this.artistsArr)
    })
    .catch(erro => {
    console.log("歌手信息获取异常：" + erro)
    })
  }
}
</script>

<style scoped>
.artists{
  padding: 0 17px;
  background: #fff;
}

.list li{
  padding-left: 0;
  min-height: 70px;
  display: flex;
  align-items: center;
  border-bottom: 1px solid #f2f2f2;
}

.pic{
  width: 54px;
  height: 54px;
  margin-right: 15px;
}

.info{
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  justify-content: flex-start;
  font-size: 16px;
}

.pic img{
  border-radius: 27px;
  overflow: hidden;
}

</style>
