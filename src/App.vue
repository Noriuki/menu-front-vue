<template>
  <v-app>
    <v-app-bar
      app
      color="#6D4C41"
      id="nav"
    >
      <div class="d-flex align-center">
        <router-link to="/">
          <v-img
            alt="Cafeteria Logo"
            class="shrink ml-10"
            contain
            src="./assets/img/logo-cafeteria.png"
            transition="scale-transition"
            width="80"
          />
        </router-link>

      </div>

      <v-spacer></v-spacer>

      <v-btn  text v-if="!isLoggedIn"
              color="#6D4C41" class="mr-10">

        <router-link to="/login">Login</router-link>

      </v-btn>

      <v-btn  text v-if="isLoggedIn"
              color="#6D4C41" class="mr-5">

        <router-link to="/admin">Admin</router-link>

      </v-btn>

      <v-btn  text v-if="isLoggedIn"
              color="#6D4C41" class="mr-5">

        <a @click="logout">Logout</a>
        
      </v-btn>

    </v-app-bar>

    <v-content>
      <router-view/>
    </v-content>

    <v-footer absolute class="font-weight-medium" color="#3E2723">
      <v-col
        class="text-center"
        cols="12"
      >
        {{ new Date().getFullYear() }} — <strong>Noriuki</strong>
      </v-col>
    </v-footer>
  </v-app>
</template>

<script>

export default {
  name: 'App',
  computed : {
      isLoggedIn : function(){ return this.$store.getters.isLoggedIn}
    },
    methods: {
      logout: function () {
        this.$store.dispatch('logout')
        .then(() => {
          this.$router.push('/login')
        })
      }
    },
    created: function () {
      this.$http.interceptors.response.use(undefined, function (err) {
        return new Promise(function (resolve, reject) {
          if (err.status === 401 && err.config && !err.config.__isRetryRequest) {
            resolve(this.$store.dispatch(logout))
          }
          reject(err);
        });
      });
    }
};
</script>

<style>
  #nav a{
    text-decoration: none;
    color: white;
  }
</style>
