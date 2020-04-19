<template>
  <!-- Hero Section Begin -->
  <section class="hero-section">
    <carousel class="hero-items" :items="1" :nav="false" :dots="false">
      <div
        class="single-hero-items set-bg"
        data-setbg="img/hero-1.jpg"
        style="background-image : url('/img/hero-1.jpg')"
      >
        <div class="container">
          <div class="row">
            <div class="col-lg-5">
              <span>Toy Kids</span>
              <h1>Promo Lebaran</h1>
              <p>Dapatkan harga khusus setiap pembelian, dibulan ramadhan ini banyak hadiah - hadiah menanti anda!!</p>
              <a href="#" class="primary-btn">Shop Now</a>
            </div>
          </div>
        </div>
      </div>
      <div
        class="single-hero-items set-bg"
        data-setbg="img/hero-1.jpg"
        style="background-image : url('/img/hero-2.jpg')"
      >
        <div class="container">
          <div class="row">
            <div class="col-lg-5">
              <span>Bag,kids</span>
              <h1>Black friday</h1>
              <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore</p>
              <a href="#" class="primary-btn">Shop Now</a>
            </div>
          </div>
        </div>
      </div>
      <div
        class="single-hero-items set-bg"
        data-setbg="img/hero-1.jpg"
        style="background-image : url('/img/hero-3.jpg')"
      >
        <div class="container">
          <div class="row">
            <div class="col-lg-5">
              <span>Bag,kids</span>
              <h1>Black friday</h1>
              <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore</p>
              <a href="#" class="primary-btn">Shop Now</a>
            </div>
          </div>
        </div>
      </div>
    </carousel>
  </section>
  <!-- Hero Section End -->
</template>
<script>
import carousel from "vue-owl-carousel";
export default {
  name: "HeroCarousel",
  components: {
    carousel
  }
};
</script>