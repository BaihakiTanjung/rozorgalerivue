<template>
  <div class="home">
    <Header></Header>
    <HeroCarousel></HeroCarousel>
    <SliderCarousel></SliderCarousel>
    <InstaPhotos></InstaPhotos>
    <PartnerLogos></PartnerLogos>
    <Footer></Footer>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import Header from "@/components/Header.vue";
import HeroCarousel from "@/components/HeroCarousel.vue";
import SliderCarousel from "@/components/SliderCarousel.vue";
import InstaPhotos from "@/components/InstaPhotos.vue";
import PartnerLogos from "@/components/PartnerLogos.vue";
import Footer from "@/components/Footer.vue";

export default {
  name: "Home",
  components: {
    // HelloWorld
    Header,
    HeroCarousel,
    SliderCarousel,
    InstaPhotos,
    PartnerLogos,
    Footer
  }
};
</script>
