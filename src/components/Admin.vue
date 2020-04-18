<template>
    <div class="container">
        <form class="produtoItem" @submit.prevent="InserirProduto">

            <v-text-field type="text" v-model="novoProduto.nomeProduto" color="brown lighten-4"  label="Nome do produto"/>
            <v-text-field type="text" v-model="novoProduto.descricao" color="brown lighten-4"  label="Descrição"/>
            <v-text-field type="text" v-model="novoProduto.imgUrl" color="brown lighten-4"  label="url da imagem"/>
            <v-text-field type="number" step="0.01" v-model="novoProduto.preco" color="brown lighten-4"  label="Preço"/>

            <v-btn 	type="submit"
				    color="brown lighten-4" class="mx-auto">
			        Inserir produto
		        </v-btn>
        </form>
      <div class="manage-produtos" v-for="produto in produtos.produtos" :key="produto.idProduto + '.key' ">
          <produtoItem :produto="produto" :editing="editing"/>
      </div>

    </div>
</template>

<script>
import { mapState } from 'vuex'
import axios from 'axios'

import ProdutoItem from './ProdutoItem.vue'

export default {
  name: 'Admin',
  components: {
    ProdutoItem
  },
  data(){
    return{
      editing: false,
      novoProduto: { 
        nomeProduto: "",
        descricao: "",
        imgUrl: "",
        preco: ""
      }
    }
  },
  mounted () {
    this.$store.dispatch('ProdutosReq')
  },
  computed: mapState([
    'produtos'
  ]),
  methods: {
    InserirProduto(){
            this.novoProduto.preco = Number(this.novoProduto.preco);
            axios({
                url: 'http://localhost:5000/api/produtos',
                data: this.novoProduto, 
                headers:{
                    "authorization": "Bearer " + localStorage.getItem('token'),
                    'Content-Type': 'application/json'
                },
                method: 'POST'
            })
            .then(
                this.$store.dispatch('ProdutosReq')
            )
    }
  }

}
</script>

<style>
  .manage-produtos{
    display: flex;
    flex-direction: row;
    border: 1px solid #3E2723;
    margin-bottom: 10px;
  }
</style>
