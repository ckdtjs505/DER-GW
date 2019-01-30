<template lang="html">
  <div id="NetWorkSetting1">
    <br>
    <h1 id="title"><i class="fas fa-cog"></i>Network Setting.</h1>
    <div class="setting">
      <div id ="content">
        <b-form @submit="onSubmit" @reset="onReset" v-if="show">
          <b-form-group id="exampleInputGroup3"
                        label="NETWORK TYPE">
            <b-form-select id="exampleInput3"
                          :options="netWork"
                          required
                          v-model="form.netWork">
            </b-form-select>
          </b-form-group>
          <b-form-group id="exampleInputGroup1"
                        label="IP ADDRESS">
            <b-form-input id="exampleInput1"
                          type="text"
                          v-model="form.address"
                          required
                          placeholder="EX) 192.168.0.101">
            </b-form-input>
          </b-form-group>
          <b-form-group id="exampleInputGroup2"
                        label="SUBNET MASK">
            <b-form-input id="exampleInput2"
                          type="text"
                          v-model="form.Mask"
                          required
                          placeholder="EX) 255.255.255.0">
            </b-form-input>
          </b-form-group>
          <b-form-group id="exampleInputGroup2"
                        label="GATEWAY">
            <b-form-input id="exampleInput2"
                          type="text"
                          v-model="form.Gateway"
                          required
                          placeholder="EX) 192.168.0.1">
            </b-form-input>
          </b-form-group>
          <br>
          <b-button id = "btn" type="reset" variant="light">Reset</b-button>
          <b-button id = "btn" type="submit" class="btn btn-secondary">Modify</b-button>
          <b-button id = "btn" variant="danger" @click="Restart()">Restart NetWork</b-button>
        </b-form>
      </div>

    </div>
  </div>
</template>

<script>
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

  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      alert(JSON.stringify(this.form));
    },
    onReset(evt) {
      evt.preventDefault();
      /* Reset our form values */
      this.form.netWork = '';
      this.form.address = '';
      this.form.Mask = null;
      this.form.Gateway = [];
      /* Trick to reset/clear native browser form validation state */
      this.show = false;
      this.$nextTick(() => {
        this.show = true
      });
    },
    Restart(evt){
      console.log('Restart NetWork');
      alert('Restart NetWork');
    }
  }


};
</script>

<style media="screen">
#title {
  font-style: italic;
  font-weight: bold;
  text-decoration: underline;
}

#NetWorkSetting1 {

  background-color :#f0f0f0;

}

#content {
  font-style: italic;
  font-weight: bold;
  background-color : #f0f0f0;
}

.setting {
  display: inline-block;

  text-align: left;
  width: 100%;
  margin-top: 2rem;
}

.btn {
  font-weight: bold;
}


</style>
