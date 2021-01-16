<template>
  <main>
    <div class="container-fluid">
      <div class="row">
        <div class="col-sm-3"></div>
        <div class="col-sm-6">
          <div class="a-section">
            <div class="a-spacing-top-medium"></div>
            <h2 style="text-align: center">Update {{ product.title }}</h2>
            <form>
              <!-- category dropdown -->
              <div a-spacing-top-medium>
                <label>Category</label>
                <select class="a-select-option" v-model="categoryID">
                  <!-- :keyをつける理由はserverに転送したときに
                  cetegory._idを手がかりにデータを更新、削除するから -->
                  <!-- :valueをつける理由は入力したあたいに適当な:valueをつけて格納するため -->
                  <option
                    v-for="category in categories"
                    :value="category._id"
                    :key="category._id"
                  >
                    {{ category.type }}
                  </option>
                </select>
              </div>
              <!-- owner dropdown -->
              <div a-spacing-top-medium>
                <label>Owner</label>
                <select class="a-select-option" v-model="ownerID">
                  <option
                    v-for="owner in owners"
                    :value="owner._id"
                    :key="owner._id"
                  >
                    {{ owner.name }}
                  </option>
                </select>
              </div>
              <!-- Title input -->
              <div class="a-spacing-top-medium">
                <label style="margin-bottom: 0px">Title</label>
                <input
                  type="text"
                  class="a-input-text"
                  style="width: 100%"
                  v-model="title"
                  :placeholder="product.title"
                />
              </div>
              <!-- Price input -->
              <div class="a-spacing-top-medium">
                <label style="margin-bottom: 0px">Price</label>
                <input
                  type="number"
                  class="a-input-text"
                  style="width: 100%"
                  v-model="price"
                  :placeholder="product.price"
                />
              </div>
              <!-- StockQuantity input -->
              <div class="a-spacing-top-medium">
                <label style="margin-bottom: 0px">StockQuantity</label>
                <input
                  type="number"
                  class="a-input-text"
                  style="width: 100%"
                  v-model="stockQuantity"
                  :placeholder="product.stockQuantity"
                />
              </div>
              <!-- Description input -->
              <div class="a-spacing-top-medium">
                <label style="margin-bottom: 0px">Description</label>
                <textarea
                  style="width: 100%"
                  v-model="description"
                  :placeholder="product.description"
                />
              </div>
              <!-- photo file -->
              <div class="a-spacing-top-medium">
                <label style="margin-bottom: 0px">Add Photo</label>
                <div class="a-row a-spacing-top-medium">
                  <label class="choosefile-button">
                    <i class="fal fa-plus"></i>
                    <input type="file" @change="onFileSelected" />
                    <p style="margin-top: -70px">{{ fileName }}</p>
                  </label>
                </div>
              </div>
              <!-- Button dropdown -->
              <hr />
              <div class="a-spacing-top-large">
                <span class="a-button-register">
                  <span class="a-button-inner">
                    <span class="a-button-text" @click="onUpdateProduct"
                      >Update product</span
                    >
                  </span>
                </span>
              </div>
            </form>
          </div>
        </div>
        <div class="col-sm-3"></div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  async asyncData({ $axios, params }) {
    //失敗したときにクラッシュしないように必ずtrycatchする
    try {
      let categories = $axios.$get("http://localhost:3000/api/categories");
      let owners = $axios.$get("http://localhost:3000/api/owners");
      //${params.id}で特定のproductをひっぱってくる
      let product = $axios.$get(
        //${params.id}を入れるときは""ではなく逆かっこ``で囲む
        `http://localhost:3000/api/products/${params.id}`
      );

      //async awaitによって時間のかかるapiからのデータ取得が終わるまでまち、
      //それからPromiseを実行し、[catResponse, ownerResponse]に格納する
      //Promiseを使うときは必ずawaitをつける
      const [catResponse, ownerResponse, productResponse] = await Promise.all([
        categories,
        owners,
        product,
      ]);
      //apiから帰ってきた商品情報をログする
      console.log(productResponse);
      //oeners,productという名前でapiから帰ってきたものを格納する。
      return {
        categories: catResponse.categories,
        owners: ownerResponse.owners,
        product: productResponse.product,
      };
    } catch (error) {
      console.log(error);
    }
  },
  //asyncDataとdataの違いはasyncDataはAPIからデータを撮る場合にのみ取得する。
  //また、asyncDataはリロードする前にデータが読み込まれるのでGoogleのCrawlに引っ掛かる。
  //dataはサイト自体から入力した値の初期値などを入れておく
  data() {
    return {
      categoryID: null,
      ownerID: null,
      title: "",
      price: "",
      description: "",
      selectedFile: null,
      stockQuantity: "",
      fileName: "",
    };
  },
  methods: {
    onFileSelected(event) {
      this.selectedFile = event.target.files[0];
      console.log(this.selectedFile);
      this.fileName = event.target.files[0].name;
    },
    //上記のデータを全てまとめて、サーバーに投げる関数
    async onUpdateProduct() {
      //POSTMANのform-dataのこと。写真などのファイルもて切ると情報と一緒に送れる。写真情報がないとき,数字やテキストのみの時ははx-www-urlencodedを使う
      let data = new FormData();
      data.append("title", this.title);
      data.append("price", this.price);
      data.append("description", this.description);
      data.append("ownerID", this.ownerID);
      data.append("stockQuantity", this.stockQuantity);
      data.append("photo", this.selectedFile, this.selectedFile.name);
      //axiosはcreate nuxt appで追加ずみ
      let result = await this.$axios.$put(
        //上記のaxiosのデータとは違う場所におかなくてはいけないから。
        `http://localhost:3000/api/products/${this.$route.params.id}`,
        data
      );

      this.$router.push("/");
    },
  },
};

// has been blocked by CORS policy: Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource.
//ブラウザにサーバーから悪意のあるレスポンスが帰ってくるのは大変なので、Network Errorを出す
</script>

<style>
</style>
