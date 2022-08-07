<template>
    <!-- *chason* 主页 -->
    <div>

        <MainHeader/>


        <div class="container-fluid px-4 xl:px-10 2xl:px-[100px] py-[50px] bg-[#000000]">
            <AllRomanticMovie :videoList="videoList" />
        </div>

        <div class="container-fluid px-4 xl:px-10 2xl:px-[100px] py-[20px] bg-[#12222d] border-t-1 border-[#203544] shadow-[0_0_10px_rgba(0,0,0,0.3)]">
            <FooterBottom/>
        </div>

    </div>
</template>

<script>
const apiToken = "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJkaWQ6ZXRocjoweDk2YTQzQ0Q0MEUwZkRhODU2Q2JGOUYzN0Y5MkJkNTM2RjRlODAwNzIiLCJpc3MiOiJ3ZWIzLXN0b3JhZ2UiLCJpYXQiOjE2NTk3ODE2MjM0ODEsIm5hbWUiOiJkbW92ZSJ9.tsUlUq7BtnFAXllyM11aKLS0mIJhFJESHPUmrUQ3wdw"
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
      console.log('111', 1111);
      let _that = this
      axios.get(_that.uploadUrl, config)
        .then(function (response) {
          // handle success
          if(response.status === 200){
            _that.videoList.splice(0, _that.videoList.length, ...response.data)
            console.log(_that.videoList,12345)
          }else{
            _that.$message.error("数据请求失败")
          }
        })
        .catch(function (error) {
          // handle error
          console.log(error);
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
</style>