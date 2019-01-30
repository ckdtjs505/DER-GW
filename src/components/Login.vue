<template>
<div class="container">
  <form class="form-signin" @submit="login">
    <label for="inputPassword" class="sr-only">Password</label>
    <input type="text" v-model="id" id="inputId" class="form-control" placeholder="ID" required>
    <input type="password" v-model="password" id="inputPassword" class="form-control" placeholder="PASSWORD" required>
    <button class="btn btn-lg btn-secondary btn-block" id="btn-sign-in" type="submit">SIGN IN</button>
    <!-- <pulse-loader :loading="loading" :color="color" :size="size"></pulse-loader>  -->
  </form>
</div> <!-- /container -->
</template>

<script>
/* import PulseLoader from 'vue-spinner/src/PulseLoader.vue' */
export default {
  name: "Login",
  data: () => ({
    id: "",
    password: "",
    color: "#696161"
  }),
  methods: {
    login(evt) {
      evt.preventDefault();
      /*
        id 접근자 : this.id
        password 접근자 : this.password
      */
      this.$router.push("/about");
    }
  }
};
</script>

<style lang="css" scoped>

body {
  padding-top: 40px;
  padding-bottom: 40px;
  background-color: #eee;
}

.form-signin {
  max-width: 330px;
  padding: 15px;
  margin: 0 auto;
}
.form-signin .form-signin-heading,
.form-signin .checkbox {
  margin-bottom: 10px;
}
.form-signin .checkbox {
  font-weight: normal;
}
.form-signin .form-control {
  position: relative;
  height: auto;
  -webkit-box-sizing: border-box;
     -moz-box-sizing: border-box;
          box-sizing: border-box;
  padding: 10px;
  font-size: 16px;
}
.form-signin .form-control:focus {
  z-index: 2;
}
.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
</style>
