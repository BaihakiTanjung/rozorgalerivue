<template>
  <div class="Product">
    <Header></Header>
    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section text-left">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="breadcrumb-text product-more">
              <router-link to="/">
                <i class="fa fa-home"></i> Home
              </router-link>
              <span>Detail</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="row">
              <div class="col-lg-6">
                <div class="product-pic-zoom">
                  <img class="product-big-img" :src="gambar_default" alt />
                </div>
                <div class="product-thumbs" v-if="productDetails.galleries.length > 0">
                  <carousel
                    :dots="false"
                    :autoplay="true"
                    :nav="false"
                    :margin="15"
                    class="product-thumbs-track ps-slider"
                  >
                    <div
                      v-for="ss in productDetails.galleries"
                      :key="ss.id"
                      class="pt"
                      @click="changeImage(ss.photo)"
                      :class="ss.photo == gambar_default ? 'active' : '' "
                    >
                      <img :src="ss.photo" alt />
                    </div>
                  </carousel>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="product-details text-left">
                  <div class="pd-title">
                    <span>{{productDetails.type}}</span>
                    <h3>{{productDetails.name}}</h3>
                  </div>
                  <div class="pd-desc">
                    <p v-html="productDetails.description"></p>
                    <h4>${{productDetails.price}}</h4>
                  </div>
                  <div class="quantity">
                    <!-- <router-link to="/cart"> -->
                    <a
                      @click="saveKeranjang(productDetails.id , productDetails.name, productDetails.price, productDetails.galleries[0].photo)"
                      href
                      class="primary-btn pd-cart"
                    >Add To Cart</a>
                    <!-- </router-link> -->
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Product Shop Section End -->
    <RelatedProducts></RelatedProducts>
    <Footer></Footer>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import Header from "@/components/Header.vue";
import RelatedProducts from "@/components/RelatedProducts.vue";
import Footer from "@/components/Footer.vue";
import axios from "axios";

import carousel from "vue-owl-carousel";

export default {
  name: "Product",
  data() {
    return {
      gambar_default: "img/mickey1.jpg",
      productDetails: [],
      keranjangUser: []
    };
  },
  components: {
    // HelloWorld
    Header,
    Footer,
    carousel,
    RelatedProducts
  },
  methods: {
    changeImage(urlImage) {
      this.gambar_default = urlImage;
      console.log(this.idProduct);
    },
    setDataPicture(data) {
      // Replace object ProductDetails dengan data parameter dari api
      this.productDetails = data;
      // Replace value gambar default dengan data dari api
      this.gambar_default = data.galleries[0].photo;
    },
    saveKeranjang(idProduct, nameProduct, priceProduct, photoProduct) {
      let productStored = {
        id: idProduct,
        name: nameProduct,
        price: priceProduct,
        photo: photoProduct
      };

      this.keranjangUser.push(productStored);
      const parsed = JSON.stringify(this.keranjangUser);
      localStorage.setItem("keranjangUser", parsed);
    }
  },
  mounted() {
    if (localStorage.getItem("keranjangUser")) {
      try {
        this.keranjangUser = JSON.parse(localStorage.getItem("keranjangUser"));
      } catch (error) {
        localStorage.removeItem("keranjangUser");
      }
    }
    axios
      .get("http://localhost:8002/api/products", {
        params: {
          id: this.$route.params.id
        }
      })
      .then(res => this.setDataPicture(res.data.data))
      .catch(err => console.log(err));
  }
};
</script>
