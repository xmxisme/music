<template>
  <div>
    <MusicList :url="url" />
  </div>
</template>
  
<script>
import MusicList from '../../components/Music_List.vue'

export default{
  data(){
    //新歌榜
    return{
      url:"/playlist/track/all?id=3779629&limit=6"
    }
  },
  components:{
    MusicList
  }
}
</script>

<style>
</style>