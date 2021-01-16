<template>
  <main>
    <div class="container-fluid c-section">
      <div class="row">
        <div class="col-sm-3"></div>
        <div class="col-sm-6">
          <div class="a-section">
            <div class="a-spacing-top-medium"></div>
            <h2 style="text-align: center">Add a new Category</h2>
            <form>
              <!-- Title input -->
              <div class="a-spacing-top-medium">
                <label style="margin-bottom: 0px">Type</label>
                <input
                  type="text"
                  class="a-input-text"
                  style="width: 100%"
                  v-model="type"
                />
              </div>

              <!-- Button dropdown -->
              <hr />
              <div class="a-spacing-top-large">
                <span class="a-button-register">
                  <span class="a-button-inner">
                    <span class="a-button-text" @click="onAddCategory"
                      >Add category</span
                    >
                  </span>
                </span>
              </div>
            </form>
            <br />
            <ul class="list-group-item">
              <li v-for="category in categories" :key="category._id">
                {{ category.type }}
              </li>
            </ul>
          </div>
          <div class="col-sm-3"></div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    //失敗したときにクラッシュしないように必ずtrycatchする
    //async awaitによって時間のかかるapiからのデータ取得が終わるまでまち、
    //それからPromiseを実行し、[catResponse, ownerResponse]に格納する
    //Promiseを使うときは必ずawaitをつける
    try {
      let response = await $axios.$get("http://localhost:3000/api/categories");
      return {
        categories: response.categories,
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
      type: "",
    };
  },
  methods: {
    //上記のデータを全てまとめて、サーバーに投げる関数
    async onAddCategory() {
      try {
        //POSTMANのform-dataのこと。写真などのファイルもて切ると情報と一緒に送れる。写真情報がないとき,数字やテキストのみの時ははx-www-urlencodedを使う
        //axiosはcreate nuxt appで追加ずみ
        let data = { type: this.type };
        let response = await this.$axios.$post(
          "http://localhost:3000/api/categories",
          data
        );
        this.categories.push(data);
      } catch (error) {
        console.log(error);
      }
      // this.$router.push("/category");
    },
  },
};

// has been blocked by CORS policy: Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource.
//ブラウザにサーバーから悪意のあるレスポンスが帰ってくるのは大変なので、Network Errorを出す
</script>

<style>
</style>
