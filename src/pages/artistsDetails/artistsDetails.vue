<template lang="html">
    <div>
        <Title :name="this.$route.params.name" :avatar="this.$route.params.avatar" />
        <List :tingid="this.$route.params.tingid" />
    </div>
</template>

<script>
import Title from '../../components/details/title.vue'
import List from '../../components/details/list.vue'


export default{
    data(){
        return{

        }
    },
    mounted(){
        
    },
    components:{
        Title,
        List
    }
}
</script>

<style scoped>

</style>