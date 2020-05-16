<template>
  <!-- Women Banner Section Begin -->
  <section class="women-banner spad">
    <div class="container-fluid">
      <div class="row">
        <div class="col-lg-12 mt-5" v-if="products.length>0">
          <carousel :items="3" :nav="false" :dots="false" :autoplay="true">
            <div class="product-item" v-for="itemProduct in products" v-bind:key="itemProduct.id">
              <div
                class="pi-pic"
                v-for="fotoProduk in itemProduct.galleries"
                v-bind:key="fotoProduk.id"
              >
                <div v-if="fotoProduk.is_default==1">
                  <img v-bind:src="fotoProduk.photo" alt />
                </div>

                <ul>
                  <li class="w-icon active">
                    <a
                      href="#"
                      @click="saveKeranjang(itemProduct.id,itemProduct.name,itemProduct.price,itemProduct.galleries[0].photo)"
                    >
                      <i class="icon_bag_alt"></i>
                    </a>
                  </li>
                  <li class="quick-view">
                    <router-link v-bind:to="'/product/'+itemProduct.id">+ Quick View</router-link>
                  </li>
                </ul>
              </div>
              <div class="pi-text">
                <div class="catagory-name">{{ itemProduct.type }}</div>
                <router-link to="/product">
                  <a href="#">
                    <h5>{{ itemProduct.name }}</h5>
                  </a>
                </router-link>
                <div class="product-price">
                  Rp. {{ itemProduct.price }}
                  <span>$35.00</span>
                </div>
              </div>
            </div>
          </carousel>
        </div>

        <div class="col-lg-12" v-else>
          <p>Tidak ada product baru untuk saat ini.</p>
        </div>
      </div>
    </div>
  </section>
  <!-- Women Banner Section End -->
</template>
<script>
import carousel from "vue-owl-carousel";
import axios from "axios";
export default {
  name: "BannerShayna",
  components: { carousel },
  data() {
    return {
      products: [],
      keranjangUser: [],
      compKey: 0
    };
  },
  methods: {
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
      this.forceRerender();
    },
    forceRerender() {
      this.compKey += 1;
    }
  },
  mounted() {
    axios
      .get("http://shayna-backend.test/api/products")
      .then(res => (this.products = res.data.data.data))
      .catch(err => console.log(err));
  }
};
</script>
<style scoped>
.product-item {
  margin-right: 25px;
}
</style>
