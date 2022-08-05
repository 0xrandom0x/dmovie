<template>
  <!-- 头部  *chason* -->
  <div
    class="flex justify-between flex-col md:flex-row items-center px-[15px] md:px-[30px] xl:px-[50px] 2xl:px-[100px] mx-auto py-5 lg:py-[0px] shadow-[0_2px_18px_rgba(0,0,0,0.1)] z-999 w-full bg-[#000000]">

    <div class="flex items-center">
      <Logo logLink="/home" />
      <div class="mainmenu"></div>
      <!-- <MainMenu class="2xl:ml-[100px] ml-[50px]"/> -->
    </div>

    <div class="flex items-center mt-4 md:mt-0">
      <!-- <HeaderSearch/> -->
      <!-- <Notification/> -->
      <!-- <Profile/> -->
      <!-- <BtnDefault
                :btnLink="''"
                :btnClass="'py-[5px] px-[15px] bg-[#f4181c] text-white font-medium hover:bg-white hover:text-[#333333]'"
                :btnText="'Upload'"
                class="ml-[10px] sm:ml-[15px]"
                @click="uploadVideo"
            /> -->
      <div class="ml-[10px] sm:ml-[15px] cursor" @click="uploadVideo">
        <div
          class="text-[14px] inline-block rounded-[3px] transition-all duration-300 py-[5px] px-[15px] bg-[#f4181c] text-white font-medium hover:bg-white hover:text-[#333333]">
          Upload</div>
      </div>
      <div class="ml-[10px] sm:ml-[15px] cursor" @click="uploadVideo">
        <div
          class="text-[14px] inline-block rounded-[3px] transition-all duration-300 py-[5px] px-[15px] bg-[#f4181c] text-white font-medium hover:bg-white hover:text-[#333333]">
          Subscribe Now</div>
      </div>
      <!-- <BtnDefault
                :btnLink="'/contact'"
                :btnClass="'py-[5px] px-[15px] bg-[#f4181c] text-white font-medium hover:bg-white hover:text-[#333333]'"
                :btnText="'Subscribe Now'"
                class="ml-[10px] sm:ml-[15px]"
            /> -->
      <!-- Offcanvas Button Start -->
      <div class="lg:hidden block leading-[1rem] ml-[10px] sm:ml-[15px]">
        <button class="overflow-hidden bg-transparent h-[18px] relative w-[26px]"
          @click="mobiletoggleClass('addClass', 'show-mobile-menu')">
          <span
            class="w-full h-[2px] bg-white block my-2 transition-all before:content-[''] before:top-0 before:bottom-auto before:absolute before:left-0 before:w-full before:h-[2px] before:bg-white after:content-[''] after:absolute after:left-0 after:w-full after:h-[2px] after:bg-white after:top-auto after:bottom-0"></span>
        </button>
      </div>
      <!-- Offcanvas Button End -->
    </div>
    <el-dialog title="Upload a video" :visible.sync="dialogVisible" width="50%" center :before-close="handleClose">
      
      <div class="upload-content">
        <el-upload class="upload-demo" :on-success="handleSuccess" :file-list="fileList" drag action="https://jsonplaceholder.typicode.com/posts/" multiple>
          <i class="el-icon-upload"></i>
          <div class="el-upload__text">Drag and drop your files here, Or<em>Click</em></div>
          <!-- <div class="el-upload__tip" slot="tip">只能上传jpg/png文件，且不超过500kb</div> -->
        </el-upload>
      </div>



      <!-- <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">取 消</el-button>
        <el-button type="danger" @click="dialogVisible = false">确 定</el-button>
      </span> -->
      <canvas id="canvassrc" style="display: none"></canvas>
    </el-dialog>
  </div>

</template>

<script>
export default {
  components: {
    Logo: () => import('@/components/logo/Logo'),
    MainMenu: () => import('@/components/header/MainMenu'),
    HeaderSearch: () => import('@/components/header/HeaderSearch'),
    Notification: () => import('@/components/header/Notification'),
    Profile: () => import('@/components/header/Profile'),
    BtnDefault: () => import('@/components/buttons/BtnDefault'),
  },
  data() {
    return {
      dialogVisible: false,
      fileList: []
    };
  },
  methods: {
    handleSuccess(response, file, fileList){
      console.log('response, file, fileList', response, file, fileList);
    },
    handleClose(done) {
      this.$confirm('确认关闭？')
        .then(_ => {
          done();
        })
        .catch(_ => { });
    },
    // offcanvas mobile-menu
    mobiletoggleClass(addRemoveClass, className) {
      const el = document.querySelector('#offcanvas-menu');
      if (addRemoveClass === 'addClass') {
        el.classList.add(className);
      } else {
        el.classList.remove(className);
      }
    },
    uploadVideo() {
      this.dialogVisible = true
      console.log('112121',);
    }
  }
}
</script>
<style lang='scss'>
.mainmenu { height: 94px; }
.cursor { cursor: pointer; }
.el-dialog__wrapper .el-dialog.el-dialog--center { border-radius: 10px !important;}
.upload-content { height: 250px; padding: 0 155px; text-align: center; }
</style>