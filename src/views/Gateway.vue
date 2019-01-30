<template lang="html">
  <div class="">
      <Navigation/>
      <ContentGateway/>
  </div>


</template>

<script>
import Navigation from "@/components/Navigation.vue";
import ContentGateway from "@/components/ContentGateway.vue";
export default {
  components : {
    Navigation,
    ContentGateway
  }
}
</script>

<style lang="css" scoped>
</style>
