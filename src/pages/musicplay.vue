// 播放音乐
<template>
  <div class="play">
    <div class="heander">
        <div class="title">
            <router-link to="/">
                <i class="iconfont icon-shouye left"></i>
            </router-link>

            <div class="music-info">
                <!-- {{this.$route.params.songid}} -->
            <p>{{this.$route.params.songname}}</p>
            <p class="author">
                <i v-for=" item in this.$route.params.songar">
                    {{item.name}}
                    <span>/</span> 
                </i>
            </p>
            </div>
            
            <router-link to="/search"><i class="iconfont icon-sousuo right"></i></router-link>
        </div>
    </div>
    
    <div class="song-info">
        <div class="song-info-img">
            <img :src="songData[0].al.picUrl" alt="">
            <LRC :durationTime="durationTime" :currentTime="currentTime" :songid="this.$route.params.songid"/>
        </div>
        <div class="iconbox">
            <i class="iconfont icon-shoucang2 left"></i>
            <i class="box"></i>
            <i class="iconfont icon-xiazai right"></i>
        </div>
    </div>
    <div class="song">
        <!-- 音源绑定 -->
        <audio ref="player" :src="currentUrl[0].url" controls autoplay></audio>
    </div>
  </div>
  
</template>

<script>
import Vue from "vue"
import "../assets/font/iconfont.css"

// 异步加载歌词
const LRC = Vue.component("lrc",(resolve)=>require(["../components/LRC"],resolve))
// https://music.cyrilstudio.top/song/url?id=33894312
export default {
    name:"musicplay",
    data(){
        return{
            currentUrl:[
                {
                    url:"",
                }
            ],
            songData:[
                {
                    al:{
                        picUrl:"",
                    }
                }
            ],
            currentTime:0,
            durationTime:0
        }
    },
    mounted(){
         // 播放音乐网络请求
        var httpurl = this.HOST  + "/song/url?id=" + this.$route.params.songid
        this.$axios.get(httpurl)
        .then(res => {
        this.currentUrl = res.data.data
        // console.log(this.currentUrl[0])
        })
        .catch(erro => {
        console.log("播放地址请求异常：" + erro)
        })

        var songMsgUrl = this.HOST  + "/song/detail?ids=" + this.$route.params.songid
        // 歌曲详情
        this.$axios.get(songMsgUrl)
        .then(res => {
        this.songData = res.data.songs
        // console.log(res.data)
        })
        .catch(erro => {
        console.log("歌曲详情请求异常：" + erro)
        })

        this.addEventListener()
    },
    beforeDestroy(){
        this.removeEventListener()
    },
    components:{
        LRC,
    },
    methods:{
        addEventListener(){
            this.$refs.player.addEventListener('timeupdate', this._currentTime) ,
            this.$refs.player.addEventListener('canplay', this._durationTime)
        },
        removeEventListener(){
            this.$refs.player.removeEventListener('timeupdate', this._currentTime),
            this.$refs.player.removeEventListener('canplay', this._durationTime)
        },

        _currentTime(){
            // currentTime 是audio提供的获取当前播放时间的方法
            this.currentTime = this.$refs.player.currentTime
        },
        _durationTime(){
            // durationTime 是audio提供的获取歌曲整体时间的方法
            this.durationTime = this.$refs.player.duration
        }
    }
}
</script>

<style scpoed>
.header{
    display: flex;
    justify-content: center;
    padding: 15px;
}

.music-info{
    flex: 1;
    font-size: 20px;
}

.title{
    display: flex;
    text-align: center;
}

.left{
    font-size: 30px;
}

.ca{
    color: red;
}

.right{
    font-size: 30px;
}

.song-info{
    padding: 15px;
}

.song-info-img{
    text-align: center;
}

.song-info-img img{
    width: 50%;
    border-radius: 5px;
    box-shadow: 0 0 10px 0 rgba(50, 50, 50, 31);
}

.song-lrc{
    margin-top: 10px;
    min-height: 50px;
}

.iconbox{
    display: flex;
    margin-top: 30px;
}

.iconbox .box{
    flex: 1;
}

.song{
    width: 100%;
    text-align: center;
}

.song audio{
    width: 80%;
}

.active{
    color: #222;
}

.author{
    font-size: 12px;
    color: #999;
}
.author i:last-child span{
    display: none;
}
</style>