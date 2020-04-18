<template>
    <div class="produtoItem">
        <div v-if="!editing">
                <p>Nome do produto: <strong>{{ produto.nomeProduto }}</strong> </p>
                <p>Descrição: <strong> {{ produto.descricao }} </strong><p>
                <p>Preço: <strong>{{ produto.preco }} </strong></p>
                <button v-if="!editing" @click="editing = !editing" class="btn btn-outline-primary border-0 ml-2">
                    <v-icon>mdi-pencil</v-icon>
                </button>
                <button v-if="!editing" @click="deleteProduto" class="btn btn-outline-primary border-0 ml-2">
                    <v-icon>mdi-delete</v-icon>
                </button>
        </div>
        <form v-else @submit.prevent="editProdutoReq" class="produtoItem">

            <v-text-field type="text" color="brown lighten-4"  v-model="produto.nomeProduto"/>
            <v-text-field type="text" color="brown lighten-4"  v-model="produto.descricao"/>
            <v-text-field type="text" color="brown lighten-4"  v-model="produto.preco"/>

            <v-btn 	type="submit"
				    color="brown lighten-4" class="mx-auto">
			    Editar
		    </v-btn>
        </form>

    </div>
</template>

<script>
import axios from 'axios'
export default {
    name:"ProdutoItem",
    props: [
        'produto',
        'editing'
    ],
    methods:{
        editProdutoReq(){
            this.$props.produto.preco = Number(this.$props.produto.preco) 
            axios({
                url: 'http://localhost:5000/api/produtos/'+ this.$props.produto.idProduto,
                data: this.$props.produto, 
                headers:{
                    "authorization": "Bearer " + localStorage.getItem('token'),
                    'Content-Type': 'application/json'
                },
                method: 'PUT'
            })
            .then(
                this.$props.editing = false
            )
        },
        deleteProduto(){
            axios({
                url: 'http://localhost:5000/api/produtos/'+ this.$props.produto.idProduto,
                data: {}, 
                headers:{
                    "authorization": "Bearer " + localStorage.getItem('token'),
                    'Content-Type': 'application/json'
                },
                method: 'DELETE'
            })
            .then(
                this.$store.dispatch('ProdutosReq')
            )
        }
    }
}
</script>

<style>
.produtoItem{
    padding: 5px;
    width: 100%;
    margin: auto;
    display: flex;
    flex-direction: row;
}
form.produtoItem {
    flex-direction: column;
    margin-bottom: 5px;
    width: 80%;
    margin: 5px auto;
}
</style>