<template>
  <nav class="navbar navbar-expand-lg bg-body-tertiary">
    <div class="container-fluid">
      <router-link to="/" class="navbar-brand">Home</router-link>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link to="/about" class="nav-link active" aria-current="page">About</router-link>
            <!-- <a class="nav-link active" aria-current="page" href="#">Home</a> -->
          </li>
          <li class="nav-item">
            <router-link to="/article" class="nav-link active" aria-current="page">Article</router-link>
          </li>
          <li class="nav-item">
            <a class="nav-link disabled" aria-disabled="true">Disabled</a>
          </li>
        </ul>
        <div v-if="!isLoggedIn">
          <div class="d-flex" role="search">
            <router-link class="btn btn-outline-primary" to="/login">Login</router-link>
            <!-- <button class="btn btn-outline-success" type="submit">Login</button> -->
          </div>
        </div>
        <div v-else>
          <span class="me-2 mt-2"><strong>Halo, {{userEmail}}</strong></span>
          <button @click="logout" class="btn btn-outline-success">Logout</button>
        </div>
      </div>
    </div>
  </nav>
  <div class="container">
      <div class="row mt-3">
        <div class="col">
          <div class="card">
            <div class="card-body">
              <router-view></router-view>
              This is some text within a card body.
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script>

export default {
  data() {
    return {
      isLoggedIn: false,
      userEmail:''
    }
  },
  created() {
    this.checkLoginStatus();
  },
  methods: {
    checkLoginStatus() {
      const user = JSON.parse(localStorage.getItem("user"));
      if (user && user.token) {
        this.isLoggedIn = true;
        this.userEmail = user.email;
      } else {
        this.isLoggedIn = false;
      }
    },
    logout() {
      localStorage.removeItem("user");
      this.isLoggedIn = false;
      this.$router.push('/login')
    }
  },
};
</script>

<style></style>
