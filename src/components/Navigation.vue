<template lang="html">
  <b-navbar toggleable="md" type="dark" variant="dark">

    <b-navbar-toggle target="nav_collapse"></b-navbar-toggle>

    <b-navbar-brand href="#">DER-GW</b-navbar-brand>

    <b-collapse is-nav id="nav_collapse">

      <b-navbar-nav>
        <b-nav-item href="#" @click="onclickNetWork">NetWork</b-nav-item>
        <b-nav-item href="#" @click="onclickGateway">Gateway</b-nav-item>
        <b-nav-item href="#" @click="onclickTransport">Device Transport</b-nav-item>
        <b-nav-item href="#" @click="onclickModels">Resource Models</b-nav-item>
        <b-nav-item href="#" @click="onclickDevices">Resource Devices</b-nav-item>
      </b-navbar-nav>

    </b-collapse>
  </b-navbar>
</template>

<script>

export default {
  data: () => ({


  }),
  methods: {
    onclickNetWork: function() {
      this.$router.push('/About');
    },
    onclickGateway: function() {
      this.$router.push('/Gateway');
    },
    onclickTransport: function() {
      this.$router.push('/Transport');
    },
    onclickModels: function() {
      this.$router.push('/Models');
    },
    onclickDevices: function() {
      this.$router.push('/Devices');
    },
  }

};
</script>

<style lang="css" scoped>
</style>
