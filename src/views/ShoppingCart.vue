<template>
  <div class="shopping-cart">
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
              <span>Shopping Cart</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Shopping Cart Section Begin -->
    <section class="shopping-cart spad">
      <div class="container">
        <div class="row">
          <div class="col-lg-8">
            <div class="row">
              <div class="col-lg-12">
                <div class="cart-table">
                  <table>
                    <thead>
                      <tr>
                        <th>Image</th>
                        <th class="p-name text-center">Product Name</th>
                        <th>Price</th>
                        <th>Action</th>
                      </tr>
                    </thead>
                    <tbody v-if="keranjangUser.length>0">
                      <tr v-for="item in keranjangUser" :key="item.id">
                        <td class="cart-pic first-row">
                          <img class="item-pic" :src="item.photo" />
                        </td>
                        <td class="cart-title first-row text-center">
                          <h5>{{ item.name }}</h5>
                        </td>
                        <td class="p-price first-row">Rp. {{item.price}} x {{item.banyak}}</td>
                        <td class="delete-item">
                          <a href="#">
                            <i class="material-icons" @click="removeItem(item.id)">close</i>
                          </a>
                        </td>
                      </tr>
                    </tbody>
                    <tbody v-else>
                      <tr>
                        <td>Tidak ada item</td>
                      </tr>
                    </tbody>
                  </table>
                </div>
              </div>
              <div class="col-lg-8 text-left">
                <h4 class="mb-4">Informasi Pembeli:</h4>
                <div class="user-checkout">
                  <form>
                    <div class="form-group">
                      <label for="namaLengkap">Nama lengkap</label>
                      <input
                        type="text"
                        class="form-control"
                        id="namaLengkap"
                        aria-describedby="namaHelp"
                        placeholder="Masukan Nama"
                        v-model="customerInfo.name"
                      />
                    </div>
                    <div class="form-group">
                      <label for="namaLengkap">Email Address</label>
                      <input
                        type="email"
                        class="form-control"
                        id="emailAddress"
                        aria-describedby="emailHelp"
                        placeholder="Masukan Email"
                        v-model="customerInfo.email"
                      />
                    </div>
                    <div class="form-group">
                      <label for="namaLengkap">No. HP</label>
                      <input
                        type="text"
                        class="form-control"
                        id="noHP"
                        aria-describedby="noHPHelp"
                        placeholder="Masukan No. HP"
                        v-model="customerInfo.number"
                      />
                    </div>
                    <div class="form-group">
                      <label for="alamatLengkap">Alamat Lengkap</label>
                      <textarea
                        class="form-control"
                        id="alamatLengkap"
                        rows="3"
                        v-model="customerInfo.address"
                      ></textarea>
                    </div>
                  </form>
                </div>
              </div>
            </div>
          </div>
          <div class="col-lg-4">
            <div class="row">
              <div class="col-lg-12">
                <div class="proceed-checkout text-left">
                  <ul>
                    <li class="subtotal">
                      ID Transaction
                      <span>#SH12000</span>
                    </li>
                    <li class="subtotal mt-3">
                      Subtotal
                      <span>Rp. {{totalHarga}}</span>
                    </li>
                    <li class="subtotal mt-3">
                      Pajak
                      <span>10%</span>
                    </li>
                    <li class="subtotal mt-3">
                      Total Biaya
                      <span>Rp. {{ totalBiaya }}</span>
                    </li>
                    <li class="subtotal mt-3">
                      Bank Transfer
                      <span>Mandiri</span>
                    </li>
                    <li class="subtotal mt-3">
                      No. Rekening
                      <span>2208 1996 1403</span>
                    </li>
                    <li class="subtotal mt-3">
                      Nama Penerima
                      <span>Shayna</span>
                    </li>
                  </ul>
                  <a href="#" @click="checkout" class="proceed-btn">I ALREADY PAID</a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Shopping Cart Section End -->
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";

import HeaderShayna from "@/components/HeaderShayna.vue";
import axios from "axios";

export default {
  name: "cart",
  components: {
    HeaderShayna
  },
  data() {
    return {
      keranjangUser: [],
      customerInfo: {
        name: "",
        email: "",
        number: "",
        address: ""
      }
    };
  },
  methods: {
    removeItem(idx) {
      // mengambil data keranjangUser dari localStorage
      let keranjangUserStorage = JSON.parse(
        localStorage.getItem("keranjangUser")
      );
      // memilih tiap nilai array, lalu mencari tiap id nya
      let itemKeranjangUserStorage = keranjangUserStorage.map(
        itemKeranjangUserStorage => itemKeranjangUserStorage.id
      );
      // membuat index dan mencari berdasar id
      let index = itemKeranjangUserStorage.findIndex(id => id == idx);
      this.keranjangUser.splice(index, 1);

      const parsed = JSON.stringify(this.keranjangUser);
      localStorage.setItem("keranjangUser", parsed);
      window.location.reload;
    },
    // checkout
    checkout() {
      let productIds = this.keranjangUser.map(function(product) {
        return product.id;
      });
      let checkoutData = {
        name: this.customerInfo.name,
        email: this.customerInfo.email,
        number: this.customerInfo.number,
        address: this.customerInfo.address,
        transaction_total: this.totalBiaya,
        transaction_status: "PENDING",
        transaction_details: productIds
      };
      axios
        .post("http://shayna-backend.test/api/checkout", checkoutData)
        .then(() => this.$router.push("success"))
        .catch(err => console.log(err));
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
  },
  computed: {
    totalHarga() {
      return this.keranjangUser.reduce(function(items, data) {
        return items + data.price;
      }, 0);
    },
    tambahPajak() {
      return (this.totalHarga * 10) / 100;
    },
    totalBiaya() {
      return this.totalHarga + this.tambahPajak;
    }
  }
};
</script>
<style scoped>
.item-pic {
  height: 80px;
}
</style>
