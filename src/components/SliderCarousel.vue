<template>
  <div>
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
      <div class="container-fluid">
        <div class="row">
          <div v-if="products.length > 0" class="col-lg-12 mt-5">
            <carousel
              class="product-slider"
              :nav="false"
              :dots="false"
              :autoplay="true"
              :margin="25"
            >
              <div v-for="ItemProduct in products" :key="ItemProduct.id" class="product-item">
                <div class="pi-pic">
                  <img :src="ItemProduct.galleries[0].photo" alt />
                  <ul>
                    <li
                      @click="saveKeranjang(ItemProduct.id , ItemProduct.name, ItemProduct.price, ItemProduct.galleries[0].photo)"
                      class="w-icon active"
                    >
                      <a href="#">
                        <i class="icon_bag_alt"></i>
                      </a>
                    </li>
                    <li class="quick-view">
                      <router-link :to="'/product/'+ItemProduct.id">+ Quick View</router-link>
                    </li>
                  </ul>
                </div>
                <div class="pi-text">
                  <div class="catagory-name">{{ItemProduct.type}}</div>
                  <router-link to="/product">
                    <h5>{{ItemProduct.name}}</h5>
                  </router-link>
                  <div class="product-price">
                    {{ItemProduct.price}}.99$
                    <!-- <span>$35.00</span> -->
                  </div>
                </div>
              </div>
            </carousel>
          </div>
          <div v-else class="col-lg-12 mt-5">
            <p>Product terbaru tidak tersedia.</p>
          </div>
        </div>
      </div>
    </section>
    <!-- Women Banner Section End -->
  </div>
</template>
<script>
import carousel from "vue-owl-carousel";
import axios from "axios";
export default {
  name: "SliderCarousel",
  components: {
    carousel
  },
  data() {
    return {
      products: [],
      keranjangUser: []
    };
  },
  methods: {
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

      window.location.reload();
    }
  },
  mounted() {
    axios
      .get("http://localhost:8002/api/products")
      .then(res => (this.products = res.data.data.data))
      .catch(err => console.log(err));
    if (localStorage.getItem("keranjangUser")) {
      try {
        this.keranjangUser = JSON.parse(localStorage.getItem("keranjangUser"));
      } catch (error) {
        localStorage.removeItem("keranjangUser");
      }
    }
  }
};
</script>
<style>
.product-item .pi-pic img {
  max-height: 555px;
}
/* .product-item {
  margin-right: 25px;
} */
</style>