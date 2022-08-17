<template>
    <!-- *chason* 主页 -->
    <div>

        <MainHeader/>


        <div class="container-fluid px-4 xl:px-10 2xl:px-[100px] py-[50px] bg-[#000000] minVideo">
            <AllRomanticMovie :videoList="videoList" />
        </div>

        <div class="container-fluid px-4 xl:px-10 2xl:px-[100px] py-[20px] bg-[#12222d] border-t-1 border-[#203544] shadow-[0_0_10px_rgba(0,0,0,0.3)]">
            <FooterBottom/>
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
.minVideo { min-height: 600px; }
</style>
