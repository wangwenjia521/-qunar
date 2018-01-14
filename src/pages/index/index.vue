<template>
  <div>
    <index-header></index-header>
    <index-swiper :list="swiperInfo"></index-swiper>
     <index-icons :list="iconInfo">icons</index-icons>
  </div>
</template>

<script>
  import IndexHeader from './header.vue'
  import IndexSwiper from './swiper.vue'
  import IndexIcons from './icons'
  import axios from 'axios'
  export default {
    name: 'Index',
    components: {
      IndexHeader,
      IndexSwiper,
      IndexIcons
    },
    data () {
      return {
        swiperInfo: [],
        iconInfo: []
      }
    },
    methods: {
      getIndexData () {
        axios.get('/api/index.json')
          .then(this.handleGetDataSucc.bind(this))
          .catch(this.handleGetDataErr.bind(this))
      },
      handleGetDataSucc (res) {
        const data = res.data.data
        this.swiperInfo = data.swiperList
        this.iconInfo = data.iconList
      },
      handleGetDataErr () {
        console.log('error')
      }
    },
    created () {
      this.getIndexData()
    }
  }
</script>
<style >

</style>


