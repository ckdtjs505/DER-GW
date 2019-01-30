<template lang="html">
  <div class="">
      <Navigation/>
      <DeviceTransport/>
  </div>


</template>

<script>
import Navigation from "@/components/Navigation.vue";
import DeviceTransport from "@/components/DeviceTransport.vue";
export default {
  components : {
    Navigation,
    DeviceTransport
  }
}
</script>

<style lang="css" scoped>
</style>
