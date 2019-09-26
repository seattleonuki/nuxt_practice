<template>
<!-- ホットリローディング = 変更を保存しただけでコンパイルが自動で走ってブラウザ上でも反映される -->
  <section class="container">
    
    <hr>
    <router-link to="/price">price page</router-link>
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
    <hr>

    <div>
      <!-- <p>{{ $store.state.message }}</p> -->
      <p>{{ $store.state.hello.message }}</p>
      <!-- mutationを使うにはcommitメソッドを使う。第一引数：mutation側で定義されている関数、第二引数：mutation側に渡したい値を入れる -->
      <!-- <v-btn fab @click="$store.commit('updateMessage', 'Commit with payload')">Update</v-btn> -->
      <!-- <v-btn fab @click="$store.dispatch('updateMessageAction', 'Dispatch with payload')">Dispatch</v-btn> -->
      <v-btn fab @click="$store.dispatch('hello/updateMessageAction', 'Dispatch with payload')">Dispatch</v-btn>
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
    return axios.get(url)  // APIからのデータ取得をリクエスト → レスポンスを受け取った段階（リクエストが成功した場合）でthenメソッドが呼ばれる
      .then((res) => {  // res = サーバーからのレスポンスデータが入っている
        return { users : res.data }  // サーバーから取得したJSONテキストをaxiosが自動的にJSのオブジェクト変換してくれる
      })
      .catch((e => {
        error({ users : e.response.status, message : 'Error!' })  // データ取得に失敗した場合のエラーハンドリング
      }))
  }
}
</script>
<style>
</style>