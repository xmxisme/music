<template>
<div class="more-list">
    <!-- {{this.$route.params.musictitle}}:{{this.$route.params.musicid}} -->
    <div class="wrapper">
        <h3>{{ this.$route.params.musictitle }}</h3>
       <VuePullRefresh :on-refresh="onRefresh">
        <router-link tag="div" :to="{name:'MusicPlay',params:{songid:item.id,songname:item.name,songar:item.ar}}" class="info url log" v-for="(item,index) in moreListData" :key="index">
            <div class="poster">
                <img :src="item.al.picUrl" alt="">
            </div>
            <div class="text-wrap">
                <div class="title">{{item.name}}</div>
                <!-- 多作者 -->
                <div class="author">
                    <span v-for="(item,index) in item.ar" :key="index">
                        {{item.name}} <span> /</span>
                    </span>
                </div>
            </div>
        </router-link>
        </VuePullRefresh>
    </div>
</div>
  
</template>

<script>
import VuePullRefresh from 'vue-pull-refresh'
export default {
    name: 'MoreList',
    data(){
        return{
            moreListData:[],
            offset:0,
            id:0
        }
    },
    components:{
        VuePullRefresh,
    },
    created(){
        this.id = this.$route.params.musicid
    },
    mounted(){
        // 热歌榜 取前12
    var httpurl = this.HOST  + "/playlist/track/all?id="+ this.$route.params.musicid +"&limit=12&offset=" + this.offset
    // console.log(httpurl)
    this.$axios.get(httpurl)
    .then(res => {
      this.moreListData = res.data.songs
    })
    .catch(erro => {
      console.log(erro)
    })
    },
    methods:{
        // 下拉刷新
        onRefresh(){
            var that = this
            const moreListUrl = this.HOST  + "/playlist/track/all?id="+ this.$route.params.musicid +"&limit=12&offset=" + this.offset
            return new Promise(function(resolve, reject) {
                setTimeout( () =>{
                    that.$axios.get(moreListUrl)
                    .then(res =>{
                        that.offset += 12
                        that.moreListData = res.data.songs
                        resolve()
                    })
                    .catch(error => {
                        console.log(error)
                    })
                })
            })
        }
    }
}
</script>

<style lang="css" scoped>
.wrapper{
    padding-top: 13px;
    text-align: center;
    margin-bottom: 10px;
    background: #fff;
    clear: both;
    overflow: hidden;
}

h3{
    font-size: 22px;
    text-align: left;
    margin-left: 17px;
    margin-bottom: 5px;
}

.wrapper .info{
    width: 43%;
    float: left;
    /* text-align: center; */
    padding-left: 17px;
    display: block;
    text-align: left;
    margin-bottom: 20px;
    position: relative;

}
.author span:last-child span{
    display: none;
}
.title{
    /* text-align: center; */
    line-height: 25PX;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    word-wrap: normal;
    color: #000;
}
.author{
    line-height: 15PX;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    word-wrap: normal;
    color: #666;
}
</style>