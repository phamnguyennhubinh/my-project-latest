<template>
  <div id="main">
    <section class="container">
      <div class="grid card shadow">
        <a-breadcrumb class="bread_crumb">
          <a-breadcrumb-item>Home</a-breadcrumb-item>
          <a-breadcrumb-item
            ><a href="http://localhost:8080/shop">Shop</a></a-breadcrumb-item
          >
          <a-breadcrumb-item
            ><a href="http://localhost:8080/shop/detail"
              >Detail</a
            ></a-breadcrumb-item
          >
          <a-breadcrumb-item
            ><a href="http://localhost:8080/shop/detail"
              >{{ counterStore.product.name }}</a
            ></a-breadcrumb-item
          >
        </a-breadcrumb>
        <div class="row">
          <!-- <div class="col-md-5">
            <div class="flex flex-column">
              <div>
                <div class="picdetail">
                  <a-image-preview-group>
                    <a-image class="picMain" :src="counterStore.product.pic">
                    </a-image>
                  </a-image-preview-group>
                </div>
              </div>
              <div class="grid">
                <div class="row _margin">
                  <div class="col-md-3">
                    <a-image :src="counterStore.product.pic"></a-image>
                  </div>
                  <div class="col-md-3">
                    <a-image :src="counterStore.product.pic"></a-image>
                  </div>
                  <div class="col-md-3">
                    <a-image :src="counterStore.product.pic"></a-image>
                  </div>
                  <div class="col-md-3">
                    <a-image :src="counterStore.product.pic"></a-image>
                  </div>
                 
                  <button class="icon-button button-arrow-1" tabindex="-1">
                    <i class="fas fa-angle-left"></i>
                  </button>
                  <button class="icon-button button-arrow-2" tabindex="-1">
                    <i class="fas fa-angle-right"></i>
                  </button>
                </div>
              </div>
            </div>
          </div> -->
          <div class="col-md-5">
            <a-carousel arrows dots-class="slick-dots slick-thumb " class="margin-top-30">
              <template #customPaging="props">
                <a>
                  <img :src="getImage(props.i)" />
                </a>
              </template>
              <div v-for="item in carouselPic" :key="item">
                <img :src="item"/>
              </div>
            </a-carousel>
          </div>
          <div class="col-md-7">
            <h3 class="nameProduct can-le-respon-1">
              <span class="like">Yêu thích</span>&nbsp;{{
                counterStore.product.name
              }}
            </h3>
            <div class="can-le-trai can-le-respon">
              {{ value }}
              <a-rate v-model:value="value" allowHalf class="changeRes"></a-rate>
              <a href="#">&nbsp;&nbsp;| 704 Đánh giá</a>
              &nbsp; | &nbsp; 2,5k Đã bán
            </div>
            <div class="price-discount-background can-le-trai">
              <div class="margin-top-30 text-align-center-res">
                <span class="price-discount margin-left-20">{{ counterStore.product.price*2 }}</span>
                <span class="price">
                  &nbsp;{{ counterStore.product.price }}&nbsp;&nbsp;</span
                >
                <span class="discount">50% GIẢM</span>
                <div class="flex items-center">
                  <i
                    class="fas fa-comments"
                    style="color: orangered; padding-left: 20px"
                  ></i>
                  <div class="padding-left-20">
                    <p style="color: orangered; margin-bottom: 0">Gì cũng rẻ</p>
                    <p>Giá tốt nhất so với sản phẩm cùng loại trên Shopee!</p>
                  </div>
                </div>
              </div>
            </div>
            <div class="flex items-center margin-top-20">
              <span class="padding-left-20">Vận Chuyển</span>
              <i class="fas fa-truck padding-0-20"></i>
              <div class="margin-right-20">
                <div>Vận chuyển Tới</div>
                <div>Phí Vận Chuyển</div>
              </div>
              <div>
                <div>
                  <a-select
                    v-model:value="value2"
                    class="width-option"
                    :dropdown-match-select-width="false"
                    :placement="placement"
                  >
                    <a-select-option value="HangZhou"
                      >P4, Gò Vấp</a-select-option
                    >
                    <a-select-option value="NingBo"
                      >P5, Tân Bình</a-select-option
                    >
                    <a-select-option value="WenZhou"
                      >P6, Quận 1</a-select-option
                    >
                  </a-select>
                </div>
                <div>
                  <a-select
                    v-model:value="value3"
                    class="width-option"
                    :dropdown-match-select-width="false"
                    :placement="placement"
                  >
                    <a-select-option value="HangZhou1"
                      >15.00-19.000</a-select-option
                    >
                    <a-select-option value="NingBo1"
                      >18.000-20.000</a-select-option
                    >
                    <a-select-option value="WenZhou1"
                      >25.000-30.000</a-select-option
                    >
                  </a-select>
                </div>
              </div>
            </div>
            <div class="flex items-center">
              <span class="margin-0-20">Số Lượng</span>
              <div>
                <a-input-number
                  id="inputNumber"
                  v-model:value="value1"
                  :min="1"
                  :max="100"
                />
              </div>
            </div>
            <div class="margin-left-20 can-le-trai center-res">
              <button type="button" class="button-add-cart" @click="addToCart">
                <i class="fa-solid fa-cart-plus"></i>&ensp;Thêm vào giỏ hàng
              </button>
              <router-link :to="{name: 'PurchaseProducts'}">
                <button type="button" class="button-buy-now" @click="buyNow">Mua Ngay</button>
              </router-link>
              <!-- <button type="button" class="button-buy-now" @click="buyNow">Mua Ngay</button> -->
            </div>
 
 
            <div class="grid">
              <hr style="margin-right: 10px;"/>
              <div class="row bread_crumb" style="margin-right: 30px;">
                <div class="col-md-4">
                  <i class="fas fa-undo" style="color: #d0011b"></i>&nbsp; 7
                  ngày miễn phí trả hàng
                </div>
                <div class="col-md-4">
                  <i
                    class="fa-solid fa-square-check"
                    style="color: #d0011b"
                  ></i>
                  &nbsp; Hàng chính hãng 100%
                </div>
                <div class="col-md-4">
                  <i class="fa-solid fa-truck-fast" style="color: #d0011b"></i>
                  &nbsp; Miễn phí vận chuyển
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
 
 
      <section class="flex card margin-50-0 shadow">
        <h3 style="padding: 20px">CHI TIẾT SẢN PHẨM</h3>
        <div>
          <div class="flex">
            <label class="label-detail">Danh mục</label>
            <div>Sản phẩm</div>
          </div>
          <div class="flex">
            <label class="label-detail">Chất liệu</label>
            <div>Vàng</div>
          </div>
          <div class="flex">
            <label class="label-detail">Kho hàng</label>
            <div>1290</div>
          </div>
          <div class="flex padding-bottom-20">
            <label class="label-detail">Gửi từ</label>
            <div>Hà Nội</div>
          </div>
        </div>
      </section>
      <section class="flex card shadow" style="margin: 50px 0">
        <h3 style="padding: 20px">MÔ TẢ SẢN PHẨM</h3>
        <div style="padding-left: 20px;" class="padding-bottom-20">
          Gấu bông heo ôm bình sữa lợn bú bình mẫu thú nhồi bông siêu cute hàng
          cao cấp mềm mịn 28cm <br />
          THÔNG TIN SẢN PHẨM <br />- Trọng Lượng: 0,5 kg. <br />✔️ Kích thước
          cao: 30cm <br />✔️ Chất liệu: vải Nhung nhồi bông <br />✔️ Xuất xứ:
          Việt Nam <br />✔️ Chất bông mềm mại, mịn màng <br />✔️ Cho bé chơi, ôm
          ngủ hoặc trang trí phòng <br />✔️ Bông siêu mịn, ko bị xù lông khi
          giặt. <br />✔️ Sản phẩm tuyệt đối an toàn cho bé. <br />✔️ Thích hợp
          cho trẻ nhỏ, con nít lẫn người lớn vì sự êm ái khi ôm & an toàn, không
          bị đổ lông. <br />✔️ Đẹp mắt, phù hợp làm quà sinh nhật, quà tặng lễ
          tết.
        </div>
      </section>
    </section>
  </div>
  <router-view/>
 </template>
 
 
 <script setup>
 import { onMounted, ref } from "vue";
 import { useCounterStore } from "@/stores";
 import { useRoute } from "vue-router";
 import { message } from "ant-design-vue";
 import 'vue-slick-carousel/dist/vue-slick-carousel.css';
 import 'vue-slick-carousel/dist/vue-slick-carousel-theme.css';
 const counterStore = useCounterStore();
 const value = ref(4.5);
 const placement = ref("topLeft");
 const value2 = ref("HangZhou");
 const value1 = ref(1);
 const value3 = ref("HangZhou1");
 const sanphams = ref([]);
 const route = useRoute();
 // const router = useRoute();
 const carouselPic = ref([]);
 // const priceNoDiscount = Number(Number(counterStore.product.price)*2)
 // const temp = ref([]);
 onMounted(async () => {
  scrollToTop();
  const productId = route.params.id;
  await counterStore.fetchEachProduct(productId);
  console.log(counterStore.product);
  sanphams.value = counterStore.product;
  console.log(value1.value);
  carouselPic.value = counterStore.product.pic;
  for (let i = 0; i < carouselPic.value.length; i++) {
    console.log(carouselPic.value[i]);
  }
 });
 const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' });
 }
 const addToCart = async () => {
  const idCustom = JSON.parse(localStorage.getItem("idCustomer"));
  const cartId = await counterStore.fetchCartIdByCustomerId(idCustom);
  console.log("This is cartId", cartId)
  const status = await counterStore.addItemToCustomerCart(cartId,route.params.id,value1.value, idCustom);
  if(status === 200){
    message.success("Đã thêm sản phẩm vào giỏ hàng!");
  }
  else {
    message.error("Thêm sản phẩm không thành công!");
  }
  // counterStore.addToCart(sanphams.value, value1.value);
  
  // await counterStore.removeCart(idCustom);
  // const temp = {id: idCustom, cart: counterStore.listCarts};
  // console.log(temp);
  // await counterStore.addCartForAcc(temp);
 };
 const buyNow =  async () => {
  const productId = route.params.id;
  await counterStore.buyNow(productId, value1);
  // router.push({ name: "PurchaseProducts" });
  counterStore.totalBillOrder
 };
 const getImage = (i) =>{
    return carouselPic.value[i];
 }
 
 
 </script>
 
 
 <style lang="scss" scoped>
 // @import "@/assets/styles/grid.css";
 $color-main: orangered;
 .margin-bottom-20 {
  margin-bottom: 20px;
 }
 .padding-bottom-20 {
  padding-bottom: 20px;
 }
 ._margin {
  position: relative;
  margin: 20px 10px;
 }
 .icon-button {
  outline: none;
  cursor: pointer;
  font-size: 0.875rem;
  font-weight: 300;
  line-height: 1;
  letter-spacing: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background-color 0.1s cubic-bezier(0.4, 0, 0.6, 1);
 }
 .button-arrow-1 {
  position: absolute;
  width: 1.2rem;
  height: 2.5rem;
  top: 50%;
  left: 0;
  transform: translateY(-50%);
  color: #fff;
  background-color: rgba(0, 0, 0, 0.2);
  border: none;
 }
 .button-arrow-2 {
  position: absolute;
  width: 1.2rem;
  height: 2.5rem;
  top: 50%;
  right: 0;
  transform: translateY(-50%);
  color: #fff;
  background-color: rgba(0, 0, 0, 0.2);
  border: none;
 }
 .can-le-trai {
  text-align: left;
 }
 .margin-50-0 {
  margin: 50px 0;
 }
 .margin-0-20 {
  margin: 0 20px;
 }
 .width-option {
  width: 120px;
 }
 .margin-right-20 {
  margin-right: 20px;
 }
 .padding-0-20 {
  padding: 0 20px;
 }
 .color-main {
  color: $color-main;
 }
 .margin-top-20 {
  margin-top: 20px;
 }
 .margin-top-30 {
  margin-top: 30px;
 }
 .margin-left-20 {
  margin-left: 20px;
 }
 .padding-left-20 {
  padding-left: 20px;
 }
 .padding-left-20-icon {
  @extend .padding-left-20;
  color: $color-main;
 }
 .discount {
  background-color: orangered;
  color: #fff;
 }
 .price {
  color: orangered;
  font-size: 40px;
 }
 .price-discount {
  text-decoration: line-through;
 }
 .price-discount-background {
  background-color: #fafafa;
 }
 .like {
  background-color: orangered;
  color: #fff;
  font-size: 13px;
 }
 .bread_crumb {
  margin-bottom: 10px;
  margin-left: 20px;
  margin-top: 5px;
 }
 .row {
  .col-md-5 {
    text-align: center;
    justify-content: center;
    vertical-align: middle;
  }
 }
 // HIDDEN
 .label-detail {
  padding-left: 30px;
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
  color: rgba(0, 0, 0, 0.4);
  font-size: 0.875rem;
  box-sizing: border-box;
  width: 8.75rem;
  padding-right: 0.75rem;
 }
 .shadow {
  box-shadow: 0 1px 1px 0 rgba(0, 0, 0, 0.03);
 }
 .button-add-cart {
  background-color: #fef6f5;
  border: 1px solid #ee4d2d;
  padding: 10px 40px;
  font-size: 16px;
  color: #ee4d2d;
  margin-top: 20px;
  box-shadow: 0 1px 1px 0 rgba(0, 0, 0, 0.03);
  &:hover {
    background-color: #fff;
    border: 1px solid #ee4d2d;
  }
 }
 .button-buy-now {
  background-color: #ee4d2d;
  color: #fff;
  border: 1px solid #ee4d2d;
  padding: 10px 50px;
  font-size: 16px;
  margin-top: 20px;
  margin-left: 20px;
  &:hover {
    background: linear-gradient(#ee4d2d, #ff7337);
    border: 1px linear-gradient(#ee4d2d, #ff7337);
  }
 }
 a {
  text-decoration: none;
  color: black;
 }
 .items-center {
  align-items: center;
 }
 .bonus {
  width: 100%;
  box-sizing: border-box;
  padding: 1.25rem 2.1875rem 0 1.25rem;
 }
 .col-left {
  width: 450px;
  padding: 15px;
  flex-shrink: 0;
 }
 .col-right {
  flex: 1 0 auto;
  /* width: 0; */
 }
 .flex-auto {
  flex: 1 1 auto;
 }
 .picMain {
  padding-top: 30px;
 }
 .nameProduct {
  text-align: left;
  /* margin-right: 180px; */
 }
 // .container {
 //   margin: 0 45px;
 // }
 .container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
 }
 .border {
  border: 1px solid;
 }
 .flex {
  display: flex;
 }
 .picdetail {
  width: 100%;
  position: relative;
  /* padding-bottom: 100%; */
 }
 .manypic {
  display: inline-block;
  box-sizing: border-box;
 }
 // .smallPics {
 //   position: relative;
 //   align-items: center;
 //   margin-top: 3%;
 //   display: flex;
 //   justify-content: space-between;
 // }
 .pic {
  width: 100%;
  margin: 0 10px;
  cursor: pointer;
 }
 :deep(.slick-dots) {
  position: relative;
  height: auto;
  margin-top: 30px;
 }
 :deep(.slick-slide img) {
  border: 5px solid #fff;
  display: block;
  margin: auto;
  max-width: 80%;
 }
 :deep(.slick-arrow) {
  display: none !important;
 }
 :deep(.slick-thumb) {
  bottom: 0px;
 }
 :deep(.slick-thumb li) {
  width: 60px;
  height: 45px;
 }
 :deep(.slick-thumb li img) {
  width: 100%;
  height: 100%;
  display: block;
 }
 :deep .slick-thumb li.slick-active img {
  filter: grayscale(0%);
 }
 @media screen and (max-width: 576px) {
  .items-center {
    display: none;
  }
  .button-add-cart {
    padding: 10px 10px;
    // display: inline;
  }
  .button-buy-now {
    padding: 10px 10px;
    // display: inline;
  }
  .container {
    margin: 0;
    padding: 0;
  }
  .card {
    // margin-top: 0px;
    padding: 0;
  }
  .changeRes {
    display: none;
  }
  .can-le-respon {
    text-align: center;
  }
  .can-le-respon-1 {
    text-align: center;
    margin-top: 20px;
  }
  .text-align-center-res {
    text-align: center;
  }
  .margin-left-20 {
    margin-left: 10px;
  }
  .center-res {
    text-align: center;
  }
 }
 @media screen and (min-width: 768px) and (max-width: 992px) {
  .button-add-cart {
    padding: 10px 20px;
    // display: inline;
  }
  .button-buy-now {
    padding: 10px 20px;
    // display: inline;
  }
  .center-res {
    text-align: center;
  }
 }
 </style>
 
 
 
 