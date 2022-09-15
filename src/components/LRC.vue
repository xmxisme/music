// 歌词
<template>
    <div class="lrcContainer">
        <div class="lrc" ref="lrc">
            {{getAllKey}}


            <p 
                class="lrc-p" 
                :class="{active:(parseInt(currentTime) >= keyArr[index] && (parseInt(currentTime) < keyArr[index+1]))}" 
                v-for="(item,key,index) in lrcData" 
                :key="index">
                {{item}}{{srcollLrc(key,index)}}
            </p>
        </div>
    </div>
</template>

<script>
// 歌词接口
//https://music.cyrilstudio.top/lyric?id= 
export default{
    name:"lrc",
    data(){
        return{
            lrc:[],
            lrcData:{},
            keyArr:[]
        }
    },
    props:{
        songid:{
            type:[String,Number],
            default:""
        },
        currentTime:{
            type:Number,
            default:0
        },
        durationTime:{
            type:Number,
            default:0
        }
    },
    mounted(){
         // 获取歌词
        var LRCurl = this.HOST  + "/lyric?id=" + this.$route.params.songid
        this.$axios.get(LRCurl)
        .then(res => {
        this.lrc = res.data
        // console.log(this.lrc)

        // 数据格式处理
        var lyrics = res.data.lrc.lyric.split("\n")
        var lrcObj = {}
        for(var i = 0; i<lyrics.length; i++){
            var lyric = decodeURIComponent(lyrics[i]) 
            
            var timeReg = /\[\d*:\d*((\.|\:)\d*)*\]/g
            var timeRegExpArr = lyric.match(timeReg)
            if(!timeRegExpArr)continue
            var clause = lyric.replace(timeReg,'')
            for(var k=0,h=timeRegExpArr.length; k<h; k++){
                var t = timeRegExpArr[k]
                var min = Number(String(t.match(/\[\d*/i)).slice(1)),
                    sec = Number(String(t.match(/\:\d*/i)).slice(1))
                var time = min * 60 + sec
                lrcObj[time]  = clause
            }
        }
        this.lrcData = lrcObj
        // console.log(this.lrcData)
        })
        .catch(erro => {
        console.log(erro)
        })
    },
    computed:{
        getAllKey(){
            for(var i in this.lrcData){
                this.keyArr.push(i)
            }
            // console.log(this.keyArr)
        }
    },
    methods:{
        srcollLrc(key,index){
            const lrcDiv = this.$refs.lrc
            if (key < this.currentTime && key > this.currentTime - (this.keyArr[index+1] - this.keyArr[index])){
                lrcDiv.style.top = -((index-2)*30) + "px"
            }
        }
    }
}

</script>

<style scoped>

.lrcContainer{
    width: 100%;
    height: 150px;
    overflow: hidden;
    position: relative;
}

.lrc{
    width:100%;
    position: absolute;
    top: 0;
}

.active{
    color: red !important;
}

.lrc-p{
    height: 30px;
    line-height: 30px;
}

.up30{
    margin-top: -30px;
}
</style>