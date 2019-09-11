<template>
<!-- ホットリローディング = 変更を保存しただけでコンパイルが自動で走ってブラウザ上でも反映される -->
  <section class="container">
    
    <hr>
    <router-link to="/price">価格のページ</router-link>
    <p>test</p>
    <hr>
    <div>
      <!-- {{ users[0].id }}, {{ users[0].name }} -->
      <!-- fetch上書きできるかな？ -->
      <ul>
        <li v-for="user in users" :key='user.id'>
          {{ user.id }}, {{ user.name }}
        </li>
      </ul>
    </div>
    <hr>
    <div>
      <img src="~/assets/cat.jpg">
    </div>
  </section>
</template>

<script>
const axios = require('axios')
let url = 'https://jsonplaceholder.typicode.com/users'

export default {
  data: function(){
    return {
      message: 'Hello, Nuxt!'
    }
  },
  asyncData({ params, error }) {  // コンポーネントを初期化する前に非同期の処理を行えるようにするためのメソッド（Nuxtが提供）
    return axios.get(url)  // APIからのデータ取得をリクエスト → レスポンスを受け取った段階でthenメソッドが呼ばれる
      .then((res) => {  // res = サーバーからのレスポンスデータが入っている
        return { users : res.data }  // サーバーから取得したJSONテキストをaxiosが自動的にJSのオブジェクト変換してくれる
      })
      .catch((e => {
        error({ users : e.response.status, message : 'Error!' })
      }))
  }
}
</script>
<style>
</style>