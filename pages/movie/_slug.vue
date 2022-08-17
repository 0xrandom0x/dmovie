<template>
    <div>

        <MainHeader/>

        <OffcanvasSidebar :class="{'show-mobile-menu' : navOpen}" @togglenav="navOpen = !navOpen" />

        <ProductDetails :product="product" />


    </div>
</template>

<script>
import product from "@/data/new/moviedata.json";
    export default {
        components: {
            MainHeader: () => import('@/components/header/MainHeader'),
            OffcanvasSidebar: () => import('@/components/header/OffcanvasSidebar'),
            ProductDetails: () => import('@/components/product/ProductDetails'),
            FooterTop: () => import('@/components/footer/FooterTop'),
            FooterBottom: () => import('@/components/footer/FooterBottom')
        },
        data() {
            return {
                navOpen: false,
                product,
                slug: this.$route.params.slug
            }
        },
        mounted () {
            this.product = product.find(product => this.slugify(product.title) === this.slug);
        },

        methods: {
            slugify(text) {
                return text
                    .toString()
                    .toLowerCase()
                    .replace(/\s+/g, "-") // Replace spaces with -
                    .replace(/[^\w-]+/g, "") // Remove all non-word chars
                    .replace(/--+/g, "-") // Replace multiple - with single -
                    .replace(/^-+/, "") // Trim - from start of text
                    .replace(/-+$/, ""); // Trim - from end of text
            }
        },
    };
</script>
<style lang='scss'>

</style>
