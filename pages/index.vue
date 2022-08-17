<template>
    <!-- *chason* 主页 -->
    <div style="background: #000000">

        <MainHeader/>


        <div class="container-fluid px-4 xl:px-10 2xl:px-[100px] py-[50px] bg-[#000000] minVideo">
            <AllRomanticMovie :videoList="videoList" />
        </div>

    </div>
</template>

<script>
const apiToken = "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJkaWQ6ZXRocjoweDFBNmFFMDBmMjFmMURENkY5Yzc5MzI1REQyNDAzYWY5QjA2NUMwMDAiLCJpc3MiOiJ3ZWIzLXN0b3JhZ2UiLCJpYXQiOjE2NjA3MjAwMDI2NDAsIm5hbWUiOiJkbSJ9.LAwMt_zPwyH7uX0xJydVARiecrJWid10E62z0zZY5qo"
const url = "https://api.web3.storage/user/uploads"

const config = {
  headers:{
    Authorization: apiToken
  }
 }
import axios from 'axios'

export default {
    components: {
        MainHeader: () => import('@/components/header/MainHeader'),
        OffcanvasSidebar: () => import('@/components/header/OffcanvasSidebar'),
        MovieBannerSliderRomantic: () => import('@/components/banner/MovieBannerSliderRomantic'),
        AllRomanticMovie: () => import('@/components/movie/AllRomanticMovie'),
        FooterTop: () => import('@/components/footer/FooterTop'),
        FooterBottom: () => import('@/components/footer/FooterBottom')
    },
    data () {
        return {
            navOpen: false,
            uploadUrl: url,
            apiToken: apiToken,
            videoList: []
        }
    },
    created(){
      let _that = this
      axios.get(_that.uploadUrl, config)
        .then(function (response) {
          // handle success
          if(response.status === 200){
            _that.videoList.splice(0, _that.videoList.length, ...response.data)
            // console.log(_that.videoList,12345)
          }else{
            _that.$message.error("数据请求失败")
          }
        })
        .catch(function (error) {
          // handle error
          // console.log(error);
        })
        .then(function () {
          // always executed
        });
    },
    mounted() {

    },
}
</script>

<style lang='scss'>
@media screen and (min-width: 1599px){
    .minVideo { min-height: 1000px; }
}
@media screen and (max-width: 1600px) and (min-width: 1440px){
    .minVideo { min-height: 665px; }
}
@media screen and (max-width: 1439px) and (min-width: 500px){
    .minVideo { min-height: 600px; }
}
</style>
