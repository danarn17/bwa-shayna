<template>
  <div class="product">
    <HeaderShayna />

    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="breadcrumb-text product-more text-left">
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
    <section class="product-shop spad page-details text-left">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="row">
              <div class="col-lg-6">
                <div class="product-pic-zoom">
                  <img class="product-big-img" :src="default_img" alt />
                </div>
                <div class="product-thumbs" v-if="productDetails.galleries.length>0">
                  <carousel class="product-thumbs-track ps-slider" :dots="false" :nav="false">
                    <div
                      v-for="ss in productDetails.galleries"
                      :key="ss.id"
                      class="pt"
                      @click="changeImage(ss.photo)"
                      :class="ss.photo==default_img ? 'active' : ''"
                    >
                      <img :src="ss.photo" alt />
                    </div>
                  </carousel>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="product-details">
                  <div class="pd-title">
                    <span>{{ productDetails.type }}</span>
                    <h3>{{ productDetails.name }}</h3>
                  </div>
                  <div class="pd-desc" v-html="productDetails.description">
                    <h4>Rp. {{productDetails.price}}</h4>
                  </div>
                  <div class="quantity">
                    <router-link to="/cart">
                      <a
                        @click="saveKeranjang(productDetails.id,productDetails.name,productDetails.price,productDetails.galleries[0].photo)"
                        href="#"
                        class="primary-btn pd-cart"
                      >Add To Cart</a>
                    </router-link>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Product Shop Section End -->
    <RelatedProducts />

    <FooterShayna />
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";

import HeaderShayna from "@/components/HeaderShayna.vue";
import RelatedProducts from "@/components/RelatedProducts.vue";
import FooterShayna from "@/components/FooterShayna.vue";
import carousel from "vue-owl-carousel";
import axios from "axios";

export default {
  name: "Product",
  components: {
    carousel,
    HeaderShayna,
    RelatedProducts,

    FooterShayna
  },
  data() {
    return {
      default_img: "",
      thumbs: [],
      productDetails: [],
      keranjangUser: []
    };
  },
  methods: {
    changeImage(urlImage) {
      this.default_img = urlImage;
    },
    setDataAndPicture(data) {
      // set data detail
      this.productDetails = data;
      // set data gambar
      this.default_img = data.galleries[0].photo;
    },
    saveKeranjang(idProduct, nameProduct, price, photo) {
      var productStored = {
        id: idProduct,
        name: nameProduct,
        price: price,
        photo: photo
      };
      this.keranjangUser.push(productStored);
      const parsed = JSON.stringify(this.keranjangUser);
      localStorage.setItem("keranjangUser", parsed);
      window.location.reload;
    }
  },
  mounted() {
    if (localStorage.getItem("keranjangUser")) {
      try {
        this.keranjangUser = JSON.parse(localStorage.getItem("keranjangUser"));
      } catch (e) {
        localStorage.removeItem("keranjangUser");
      }
    }
    axios
      .get("http://shayna-backend.test/api/products", {
        params: {
          id: this.$route.params.id
        }
      })
      .then(res => this.setDataAndPicture(res.data.data))
      .catch(err => console.log(err));
  }
};
</script>
<style scoped>
.product-thumbs .pt {
  margin-right: 10px;
}
</style>
