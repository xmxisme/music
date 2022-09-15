<template>
  <div class="search">
    <div class="search-title">
      <input type="text" name="" placeholder="请输入搜索内容" v-model="searchContent">
      <button type="button" @click="searchHandler" name="button">搜索</button>
    </div>
    <ul class="list searchlist">
      <router-link :key="item.id" tag="li" :to="{name:'MusicPlay',params:{songid:item.id,songname:item.name,songar:item.ar}}"
      class="song" v-for="item in songList">
        <div class="left">
          <div class="info single-line">
            <div class="name">
              <span>{{item.name}}</span>
            </div>
            <span class="txt">{{item.ar[0].name}}</span>
          </div>
        </div>
      </router-link>
    </ul>
  </div>
</template>

<script>
export default{
  name:"search",
  data(){
    return{
      searchContent:"",
      songList:[
        {
          ar:[
            {
              name:""
            }
          ]
        }
      ]
    }
  },
  methods:{
    searchHandler(event){
      // 搜索歌曲
      var keyUrl = this.HOST  + "/cloudsearch?keywords=" + this.searchContent
      this.$axios.get(keyUrl)
      .then(res => {
      this.songList = res.data.result.songs
      // console.log(this.songList)
      })
      .catch(erro => {
      console.log("搜索信息获取异常：" + erro)
      })
    }
  }
}
</script>

<style scoped>
.name span{
  font-size: 18px;
}

.search-title{
  padding: 20px;
  overflow: hidden;
  clear: both;
}

input{
  width: 80%;
  height: 30px;
  line-height: 30px;
  background: #fff;
  border: 1px solid #f1f2f3;
  padding-left: 10px;
  float: left;
  display: inline-block;
}

button{
  float: left;
  width: 15%;
  height: 30px;
}

.list{
  word-wrap: break-word;
  -webkit-hyphens: auto;
  hyphens: auto;
  word-break: break-all;
  border-bottom: 1px solid #e5e5e5;
  border-top: 1px solid #e5e5e5;
}

.list li.song{
  -webkit-box-pack: justify;
  -webkit-justify-content: space-between;
  justify-content: space-between;
  min-height: 55px;
  text-align: left;
}

li{
  display: -webkit-box;
  display: -webkit-flex;
  display: flex;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
  -webkit-flex-direction: row;
  flex-direction: row;
  -webkit-box-pack: start;
  -webkit-justify-content: flex-start;
  justify-content: flex-start;
  -webkit-box-align: center;
  -webkit-algin-items: center;
  align-items: center;
  -webkit-box-flex: 1;
  flex: 1;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  min-height: 50px;
  border-bottom: 1px solid #f2f2f2;
  padding-left: 10px;

}

.list .item.song .left, .list li.song .left{
  display: -webkit-box;
  display: -webkit-flex;
  display: flex;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
  -webkit-flex-direction: row;
  flex-direction: row;
  -webkit-box-pack: start;
  -webkit-justify-content: flex-start;
  justify-content: flex-start;
  -webkit-box-align: center;
  -webkit-algin-items: center;
  align-items: center;
  -webkit-box-flex: 1;
  flex: 1;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.lsit .item .info, .list li .info{
  -webkit-box-flex: 1;
  -webkit-flex: 1;
  flex: 1;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.list li .info>span{
  font-weight: 400;
  display: block;
  font-size: 12px;
  color: #999;
}

</style>

