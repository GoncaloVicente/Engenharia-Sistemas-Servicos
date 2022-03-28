<template>
  <div id="app">
      <div v-if="loggedIn">
        <nav class="navbar navbar-dark bg-dark navbar-expand-lg fixed-top">
          <div class="container-fluid">
            <a class="navbar-brand" href="#">
              <img
                src="/logo_white.png"
                alt=""
                width="30"
                class="d-inline-block align-text-top mr-3"
              />
                ManRenewables Platform
            </a>
            <button
              class="navbar-toggler"
              type="button"
              data-bs-toggle="collapse"
              data-bs-target="#navbarNavDropdown"
              aria-controls="navbarNavDropdown"
              aria-expanded="false"
              aria-label="Toggle navigation"
            >
              <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNavDropdown">
              <div class="row">
                <div class="col">
                  <button type="button" class="btn btn-outline-warning">
                    <router-link to="/">Home</router-link>
                  </button>
                </div>
                <div class="col">
                  <button type="button" class="btn btn-outline-warning">
                    <router-link to="/about">About</router-link>
                  </button>
                </div>
                <div class="col">
                  <button type="button" class="btn btn-outline-warning">
                    <router-link to="/dashboard">Dashboard</router-link>
                  </button>
                </div>
              </div>
            </div>
          </div>
        </nav>
      <br />
      <div>
        <router-view />
      </div>
      </div>
      <LoginView v-else @logged-in="login"/>

  </div>

</template>


<script>
    import LoginView from "./views/Login.vue"

    export default {
        name: "App",
        components: {
            LoginView
        },
        data(){
          return {
            loggedIn: false,
          }
        },
        methods:{
          login(){
            this.loggedIn = true
          }
        }
    };
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
