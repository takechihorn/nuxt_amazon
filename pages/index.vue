<template>
  <main>
    <div class="a-spacing-large">
      <div class="container-fluid browsing-history">
        <div class="row">
          <!-- Grid system rowの中のカラムの合計が12 xs-smartphone sm-tablet md-PC lg-largePC
            12より少ない時は左詰 12より多い時は回り込む
            ex, col-sm-8:smタブレットより大きい時は12のうち8をとり、smタブレットより小さい場合は横並び全部とる。横画面いっぱい-->

          <div class="col-sm-8 col-8">
            <h1 class="a-size-large a-spacing-none a-text-normal">
              All products
            </h1>
            <div class="a-spacing-large"></div>
            <!-- Button -->
            <a href="#" class="a-button-buy-again">Add a new product</a>
            <a href="#" class="a-button-history margin-right-10"
              >Add a new category</a
            >
            <a href="#" class="a-button-history margin-right-10"
              >Add a new owner</a
            >
          </div>
        </div>
      </div>
      <!-- Listing page -->
      <div class="a-spacing-large"></div>
      <div class="container-fluid browsing-history">
        <div class="row">
          <!-- return {
        products: response.products,
      }; 上記のreturnのproductと連動-->
          <!-- :keyはv-bind:keyの省略。この場合productのindexがproduct_.id -->
          <div
            v-for="(product, index) in products"
            :key="product._id"
            class="col-xl-2 col-lg-2 col-md-3 col-sm-6 col-6 br bb"
          >
            <div class="history-box">
              <!-- Product image -->
              <a href="#" class="a-link-normal">
                <img :src="product.photo" alt="img-fluid" />
              </a>
              <!-- Product title -->
              <div class="a-spacing-top-base asin-title">
                <span class="a-text-normal">
                  <div class="p13n-sc-truncated">Product title</div>
                </span>
              </div>
              <!-- Product Rating -->
              <div class="a-row">
                <a href="#">
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                </a>
                <span class="a-letter-space"></span>
                <span class="a-color-tertiary a-size-small asin-reviews"
                  >(1732)</span
                >
              </div>
              <!-- Product Price -->
              <div class="a-row">
                <span class="a-size-base a-color-price">
                  <span class="p13n-sc-price">{{ product.price }}</span>
                </span>
              </div>
              <!-- Product Buttons -->
              <div class="a-row">
                <a href="#" class="a-button-history margin-right-10">Update</a>
                <a href="#" class="a-button-history margin-right-10">Delete</a>
              </div>
            </div>
          </div>
          <div class="col-xl-2 col-lg-2 col-md-3 col-sm-6 col-6 br bb">
            <div class="history-box">
              <!-- Product image -->
              <a href="#" class="a-link-normal">
                <img src="#" alt="img-fluid" />
              </a>
              <!-- Product title -->
              <div class="a-spacing-top-base asin-title">
                <span class="a-text-normal">
                  <div class="p13n-sc-truncated">Product title</div>
                </span>
              </div>
              <!-- Product Rating -->
              <div class="a-row">
                <a href="#">
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                </a>
                <span class="a-letter-space"></span>
                <span class="a-color-tertiary a-size-small asin-reviews"
                  >(1732)</span
                >
              </div>
              <!-- Product Price -->
              <div class="a-row">
                <span class="a-size-base a-color-price">
                  <span class="p13n-sc-price">$23</span>
                </span>
              </div>
              <!-- Product Buttons -->
              <div class="a-row">
                <a href="#" class="a-button-history margin-right-10">Update</a>
                <a href="#" class="a-button-history margin-right-10">Delete</a>
              </div>
            </div>
          </div>
          <div class="col-xl-2 col-lg-2 col-md-3 col-sm-6 col-6 br bb">
            <div class="history-box">
              <!-- Product image -->
              <a href="#" class="a-link-normal">
                <img src="#" alt="img-fluid" />
              </a>
              <!-- Product title -->
              <div class="a-spacing-top-base asin-title">
                <span class="a-text-normal">
                  <div class="p13n-sc-truncated">Product title</div>
                </span>
              </div>
              <!-- Product Rating -->
              <div class="a-row">
                <a href="#">
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                </a>
                <span class="a-letter-space"></span>
                <span class="a-color-tertiary a-size-small asin-reviews"
                  >(1732)</span
                >
              </div>
              <!-- Product Price -->
              <div class="a-row">
                <span class="a-size-base a-color-price">
                  <span class="p13n-sc-price">$23</span>
                </span>
              </div>
              <!-- Product Buttons -->
              <div class="a-row">
                <a href="#" class="a-button-history margin-right-10">Update</a>
                <a href="#" class="a-button-history margin-right-10">Delete</a>
              </div>
            </div>
          </div>
          <div class="col-xl-2 col-lg-2 col-md-3 col-sm-6 col-6 br bb">
            <div class="history-box">
              <!-- Product image -->
              <a href="#" class="a-link-normal">
                <img src="#" alt="img-fluid" />
              </a>
              <!-- Product title -->
              <div class="a-spacing-top-base asin-title">
                <span class="a-text-normal">
                  <div class="p13n-sc-truncated">Product title</div>
                </span>
              </div>
              <!-- Product Rating -->
              <div class="a-row">
                <a href="#">
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                  <i class="fa fa-star"></i>
                </a>
                <span class="a-letter-space"></span>
                <span class="a-color-tertiary a-size-small asin-reviews"
                  >(1732)</span
                >
              </div>
              <!-- Product Price -->
              <div class="a-row">
                <span class="a-size-base a-color-price">
                  <span class="p13n-sc-price">$23</span>
                </span>
              </div>
              <!-- Product Buttons -->
              <div class="a-row">
                <a href="#" class="a-button-history margin-right-10">Update</a>
                <a href="#" class="a-button-history margin-right-10">Delete</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  // axiosとはAPIを呼び出すLibrary
  //asyncDataとはNuxt固有の関数でローディングが完了する前にデータをフェッチする関数
  //SEOに良い。何故ならばデータが先に読み込まれるから
  async asyncData({ $axios }) {
    try {
      let response = await $axios.$get("http://localhost:3000/api/products");
      console.log(response);
      return {
        products: response.products,
      };
    } catch (error) {}
  },
};
</script>

<style>
</style>
