<template>
    <!-- *chason* 分页  -->
    <div>
        <div class="romantic-movie relative grid grid-cols-4 sm:grid-cols-4 md:grid-cols-4 lg:grid-cols-4 xl:grid-cols-4 2xl:grid-cols-4 gap-8">
            <div class="" v-for="(product, Index) in getItems" :key="Index">
                <SingleProduct 
                    :product="product"
                    :PageLink="'/movie'"
                    :btnLink="'/movie'"
                />
            </div>
        </div>
        <paginate
            :page-count="getPaginateCount"
            :prev-text="'<'"
            :next-text="'>'"
            :click-handler="paginateClickCallback"
            class="pagination-list">
        </paginate>
    </div>
</template>

<script>

// import movieData from "@/data/new/moviedata.json";
let showUrl = 'https://dweb.link/ipfs/'
export default {
  props: {
    videoList:{
      type:Array,
      default: []
    },
  },
    components: {
        SingleProduct: () => import('@/components/product/SingleProduct')
    },
    data () {
        return {
            movieSeries: [],
            currentPage: 1,
            perPage: 12,
        }
    },
    mounted () {
      
    },
    created(){
      this.getItems.splice(0, this.getItems.length)
      for(let i in 6){
        this.getItems.push({ name: 'Movie Loading', movieLink: '' })
      }
    },
    computed: {
        getItems() {
          
            let start = (this.currentPage - 1) * this.perPage;
            let end = this.currentPage * this.perPage;
            let data = this.movieSeries.slice(start, end)
            return data
        },
        getPaginateCount() {
            return Math.ceil(this.movieSeries.length / this.perPage);
        }
    },
    methods: {
        paginateClickCallback(pageNum) {
            this.currentPage = Number(pageNum);
        },
    },
    watch: {
      videoList:  {
        immediate: true,
        deep: true,
        handler(val){
          val.forEach(ele => {
            this.$set(ele, 'movieLink', showUrl + ele.cid)
            this.$set(ele, 'routerLink', 'Land And Sea')
          });
            this.movieSeries.splice(0, this.movieSeries.length, ...val)
        },
      }
    }
}
</script>

<style lang='scss'>
.newstyle-arrow {
    .swipper-arrow {
        @apply w-[30px] h-[30px] bg-[#333333] flex items-center justify-center rounded-[3px] hover:bg-red transition-all duration-500;
    }
}
.pagination-list{
    @apply flex justify-center items-center mt-8;
    li {
        &.disabled {
            @apply hidden;
        }
        &.active{
            & a {
                @apply bg-[#f4181c];
            }
        }
        a {
            @apply w-[35px] h-[35px] text-[16px] flex justify-center items-center rounded-full mx-1 text-white text-center bg-[#333333] hover:bg-[#f4181c];
        }
    }
}
</style>