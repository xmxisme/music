<template>
    <div class="art-list">
        <ul class="list">
            <router-link
             tag="li" :to="{name:'MusicPlay',params:{songid:item.id,songname:item.name,songar:item.ar}}"
             v-for="item in listArr" :key="item.id" class="song" >
             <div class="left">
                {{item.name}}
             </div>

            </router-link>
        </ul>
    </div>
</template>

<script>
export default {
    data(){
        return{
            listArr:[]
        }
    },
    props:{
        tingid:{
            type:Number,
            default:0
        }
    },
    mounted(){
        // 获取歌手热门50首歌曲
        var tingUrl = this.HOST  + "/artist/top/song?id=" + this.tingid
        this.$axios.get(tingUrl)
        .then(res => {
        this.listArr = res.data.songs
        // console.log(res.data)
        })
        .catch(erro => {
        console.log("歌手热门歌曲信息获取异常：" + erro)
        })
    }
}
</script>

<style scoped>

.art-list{
    padding: 0 17px;
}

.song{
    height: 50px;
    line-height: 50px;
    border-bottom: 1px solid #999;
    text-align: left;
}

.left{
    font-size: 18px;
}


</style>