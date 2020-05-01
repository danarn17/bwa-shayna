<template>
  <!-- Women Banner Section Begin -->
  <section class="women-banner spad">
    <div class="container-fluid">
      <div class="row">
        <div class="col-lg-12 mt-5">
          <carousel :items="3" :nav="false" :dots="false" :autoplay="true">
            <div class="product-item">
              <div class="pi-pic">
                <img src="img/products/c-gatot.jpg" alt="" />
                <ul>
                  <li class="w-icon active">
                    <a href="#"><i class="icon_bag_alt"></i></a>
                  </li>
                  <li class="quick-view">
                    <a href="product.html">+ Quick View</a>
                  </li>
                </ul>
              </div>
              <div class="pi-text">
                <div class="catagory-name">Tas Belacu</div>
                <a href="#">
                  <h5>Mahyang Gatotkaca</h5>
                </a>
                <div class="product-price">
                  $14.00
                  <span>$35.00</span>
                </div>
              </div>
            </div>
            <div class="product-item">
              <div class="pi-pic">
                <img src="img/products/w-nakula.jpg" alt="" />
                <ul>
                  <li class="w-icon active">
                    <a href="#"><i class="icon_bag_alt"></i></a>
                  </li>
                  <li class="quick-view"><a href="#">+ Quick View</a></li>
                </ul>
              </div>
              <div class="pi-text">
                <div class="catagory-name">Bags</div>
                <a href="#">
                  <h5>Mahyang Nakula</h5>
                </a>
                <div class="product-price">
                  $13.00
                </div>
              </div>
            </div>
            <div class="product-item">
              <div class="pi-pic">
                <img src="img/products/c-arjuna.jpg" alt="" />
                <ul>
                  <li class="w-icon active">
                    <a href="#"><i class="icon_bag_alt"></i></a>
                  </li>
                  <li class="quick-view"><a href="#">+ Quick View</a></li>
                </ul>
              </div>
              <div class="pi-text">
                <div class="catagory-name">Bags</div>
                <a href="#">
                  <h5>Mahyang Arjuna</h5>
                </a>
                <div class="product-price">
                  $13.00
                </div>
              </div>
            </div>
            <div class="product-item">
              <div class="pi-pic">
                <img src="img/products/w-puntadewa.jpg" alt="" />
                <ul>
                  <li class="w-icon active">
                    <a href="#"><i class="icon_bag_alt"></i></a>
                  </li>
                  <li class="quick-view"><a href="#">+ Quick View</a></li>
                </ul>
              </div>
              <div class="pi-text">
                <div class="catagory-name">Bags</div>
                <a href="#">
                  <h5>Mahyang Puntadewa</h5>
                </a>
                <div class="product-price">
                  $13.00
                </div>
              </div>
            </div>
            <div class="product-item">
              <div class="pi-pic">
                <img src="img/products/c-werkudara.jpg" alt="" />
                <ul>
                  <li class="w-icon active">
                    <a href="#"><i class="icon_bag_alt"></i></a>
                  </li>
                  <li class="quick-view"><a href="#">+ Quick View</a></li>
                </ul>
              </div>
              <div class="pi-text">
                <div class="catagory-name">Bags</div>
                <a href="#">
                  <h5>Mahyang Werkudara</h5>
                </a>
                <div class="product-price">
                  $13.00
                </div>
              </div>
            </div>
          </carousel>
        </div>
      </div>
    </div>
  </section>
  <!-- Women Banner Section End -->
</template>
<script>
import carousel from "vue-owl-carousel";
export default {
  name: "BannerShayna",
  components: { carousel },
};
</script>
<style scoped>
.product-item {
  margin-right: 25px;
}
</style>
