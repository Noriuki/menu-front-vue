<template>
    <div class="produtos-list">
      <div id="banner">
        <img src="../assets/img/banner.jpg" center width="100%" height="280">
      </div>
      <div class="produto" v-for="produto in produtos.produtos" :key="produto.nomeProduto + '.key' ">
          
        <h2> {{ produto.nomeProduto }}</h2>
        <img :src="produto.imgUrl">

        <p> {{ produto.descricao }} <p>
        <p> {{ '$ ' + produto.preco }} </p>

      </div>
    </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  name: 'Home',
  mounted () {
    this.$store.dispatch('ProdutosReq')
  },
  computed: mapState([
    'produtos'
  ])
}
</script>

<style>
#banner{
  margin: 10px auto;
  width: 96%;
}
.produtos-list{
  background: url('../assets/img/home-background.jpg') center no-repeat;
  margin: 0;
  width: 100%;
  min-height: calc(100vh - 88px);
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  padding-bottom: 60px;
}
.produto{
  margin: 10px 23px;
  padding: 10px;
  width: min-content;
  text-align: center;
  height: min-content;
  background-color: #6D4C41;
}
.produto img{
  height: 290px;
  width: 380px;
  border-radius: 5px;
}
</style>
