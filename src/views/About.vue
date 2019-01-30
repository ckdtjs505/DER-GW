<template>
<div class="about">
  <Navigation/>
  <NetWorkSetting/>
</div>
</template>

<script>
import Navigation from "@/components/Navigation.vue";
import NetWorkSetting from "@/components/NetWorkSettin.vue"

export default {
  data: () => ({
    password: "",
    color: "#696161",
    form: {
          netWork: null,
          address: '',
          Mask: '',
          Gateway: '',
        },
    netWork: [
      { text: 'Selet Network Type', value: null },
       'STATIC', 'DHCP'
    ],
    show: true
  }),
  components: {
    Navigation,
    NetWorkSetting
  }

};
</script>

<style media="screen">
#NetWorkSetting {
  display: inline-block;
  width: 600px;
  background-color: white;
  margin-top: 2rem;
}

.setting {
  display: inline-block;
  background-color: white;
  text-align: left;
  width: 300px;
}

#sel {
  background: red;
  width: 50px;
}
</style>
