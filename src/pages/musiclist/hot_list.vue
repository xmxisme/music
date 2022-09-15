<template>
  <div>
    <MusicList :url="url" />
  </div>
</template>
<script>
import MusicList from '../../components/Music_List.vue'

export default{
  data(){
    return{
      // 飙升榜
      url:"/playlist/track/all?id=19723756&limit=6"
    }
  },
  components:{
    MusicList
  }
}

</script>

<style>
</style>