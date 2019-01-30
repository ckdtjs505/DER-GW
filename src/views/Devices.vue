<template lang="html">
  <div class="">
      <Navigation/>
      <ResourceModel/>
  </div>


</template>

<script>
import Navigation from "@/components/Navigation.vue";
import ResourceModel from "@/components/ResourceModel.vue"

export default {
  components : {
    Navigation,
    ResourceModel
  }
}
</script>

<style lang="css" scoped>
</style>
