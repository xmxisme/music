<template lang="html">
  <div class="">
    <TodayRecommend title="我的歌单——R" musicid="2414242273"/>
    <NewsMusci />
    <RotationChart />
    <MusicListVav />
    <keep-alive>3778678
      <router-view />
    </keep-alive>
    <TodayRecommend title="美国Billboard排行榜" musicid="60198"/>
  </div>
    
</template>

<script>

import TodayRecommend from '../components/Today_Recommend'
import NewsMusci from '../components/News_Music'
import RotationChart from '../components/Rotation_Chart.vue'
import MusicListVav from '../pages/musiclist/music_listnav.vue'

export default{
  name:"home",
  components: {
    TodayRecommend,
    NewsMusci,
    RotationChart,
    MusicListVav,
  }
}
</script>

<style lang="css">

</style>
