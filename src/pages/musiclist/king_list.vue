<template>
  <div>
    <MusicList :url="url" />
  </div>
</template>
  
<script>
import MusicList from '../../components/Music_List.vue'

export default{
  data(){
    // 原创榜
    return{
      url:"/playlist/track/all?id=2884035&limit=6"
    }
  },
  components:{
    MusicList
  }
}
</script>

<style>
</style>