<template>

 <div class="container">
   <form id="loginForm" class="login" @submit.prevent="login">
		<h1>Login</h1>

		<v-text-field color="brown lighten-3" required v-model="Email" type="text" label="Email"/>

		<v-text-field color="brown lighten-3" required v-model="Senha" type="password" label="Senha"/>

		<v-btn 	large type="submit"
				color="brown lighten-4" class="mx-auto">
			Logar
		</v-btn>
   </form>
 </div>

</template>

<script>
	export default {
		data(){
			return {
				Email : "",
				Senha : ""
            }
		},
		methods: {
			login: function () {
				let Email = this.Email 
				let Senha = this.Senha
				this.$store.dispatch('login', { Email, Senha })
				.then(() => this.$router.push('/'))
				.catch(err => console.log(err))
			}
		}
	}
</script>

<style>
.container{
	max-width: 900px!important;
	max-height: max-content;
	display: flex;
	flex-direction: column;
	flex-wrap: wrap;
	margin: 0 auto;
	margin-bottom: 60px;
}
#loginForm{
	text-align: center;
	margin: 80px auto;
	padding: 15px;
	max-height: max-content;
	width: 500px;
	display: flex;
	flex-direction: column;
	flex-wrap: wrap;
	background-color: #EFEBE9;
	border: 1px solid #D7CCC8;
}
</style>