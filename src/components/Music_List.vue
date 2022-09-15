<template>
  <div class="board panele">
    <div class="panel hotsongs on">
        <ul class="list">
            <router-link :to="{name:'MusicPlay',params:{songid:item.id,songname:item.name,songar:item.ar}}" tag="li" class="song url" v-for="(item,index) in currendData" :key="index">
                <div class="poster">
                    <img :src="item.al.picUrl" :alt="item.name">
                </div>
                <div class="info">
                    <div class="name more">
                        {{item.name}}
                    </div>
                    <div class="author more">
                        {{item.ar[0].name}}
                    </div>
                </div>
            </router-link>
        </ul>
        <div class="more-songs url">
            查看榜单&gt;
        </div>

    </div>
  </div>
</template>

<script>
export default {
    name:"list",
    data() {
        return{
            currendData:[]
        }
    },
    props:{
        // 让页面传递url
        url:{
            type:String,
            default:""
        }
    },
    mounted(){
    var httpUrl = this.HOST  + this.url
    this.$axios.get(httpUrl)
    .then(res => {
      this.currendData = res.data.songs
    })
    .catch(erro => {
      console.log(erro)
    })
    }
}
</script>

<style scoped>

.board{
    margin-top: 10px;
    margin-bottom: 10px;
}
.panel {
    border-top: 1px solid #eee;
    position: relative;
    top: -1px;
    display: block;
    background: #fff;
}

.list{
    padding: 20px;
    padding-top: 0;
}

.panel .list li{
    height: 60px;
    border-bottom: 1px solid #eee;
    padding-left: 0;
    display: flex;
    padding-top: 10px;
}

.panel .list li .poster{
    position: relative;
    width: 45px;
    margin-right: 8px;
}

.panel .list li .poster img{
    border: 1px solid #eee;
}

.info{
    flex: 1;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}

.info .author{
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    font-size: 12px;
    color: #999;
    margin-top: 2px;
}
.more:hover{
    text-decoration: underline;
    cursor: pointer;
}

.more-songs{
    color: #999;
    margin-top: 9px;
    font-size: 12px;
    text-align: center;
    height: 32px;
    line-height: 32px;
}

</style>