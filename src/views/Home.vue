<template>
  <div class="home">
    <div id="Login">
      <img  width="100px" alt=" logo" src="../assets/icon.png">
      <Login/>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Login from "@/components/Login.vue";

export default {
  name: "home",
  components: {
    Login
  }
};
</script>

<style>
#home {

}
#Login {
  margin-top: 10rem;
  display: inline-block;
  background-color: white;

  border-radius: 10px;
  width: 350px;
}
img {
  margin-top: 1rem;
}
</style>
