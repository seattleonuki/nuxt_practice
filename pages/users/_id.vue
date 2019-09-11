<template>
    <section>
        <h1>{{ message }}</h1>
        <!-- id = ファイル名の_idと一致 -->
        <p>id: {{ this.$route.params.id }}</p>
    </section>
</template>

<script>
export default {
    data: function(){
        return {
            message: 'users/_id.vueを表示中'
        }
    },
    validate({ params }) {
        //testメソッド＝正規表現と指定された文字列の一致を判定
    return /^\d+$/.test(params.id)
    }
}
// [動的ルーティングの想定]userIDを元にAPIを叩いてuser情報を取得し、表示する
</script>