<template>
<div class="container">
  <div class="col-md-6 offset-md-3">
    <!-- title -->
    <br>
    <h1 class="text-center mb-2" id="title"><i class="fas fa-cog"></i>Gateway Setting.</h1>
    <br><br>

    <form id="form"  @submit="clickEvent()" >
      <!-- AET NAME -->
      <div class="form-group row">
        <label class="col-sm-4">AET NAME</label>
        <div class="col-sm-15">
          <input type="text" v-model="form.name" class="form-control" id="aet_name" placeholder="ex) aet1" required data-validation-required-message="Please enter your aet1">
          <p class="help-block text-danger"></p>
        </div>
      </div>

      <!-- NODE ID -->
      <div class="form-group row">
        <label class="col-sm-4">NODE ID</label>
        <div class="col-sm-15">
          <input type="text" v-model="form.node_id" class="form-control" id="node_id" placeholder="ex) 0.4a316b58511" required data-validation-required-message="Please enter your NODE ID">
          <p class="help-block text-danger"></p>
        </div>
      </div>


      <!-- HCL -->
      <div class="form-group row">
        <label class="col-sm-4">HCL</label>
        <div class="col-sm-15">
          <input type="text" v-model="form.hcl" class="form-control" id="hcl" placeholder="ex) /mobius-yt" required data-validation-required-message="Please enter your HCL">
          <p class="help-block text-danger"></p>
        </div>
      </div>

      <hr>
      <br>
      <!-- CSE ID -->
      <div class="form-group row">
        <label class="col-sm-4">CSE ID</label>
        <div class="col-sm-15">
          <input type="text" v-model="form.cse_id" class="form-control" id="cse_id" placeholder="ex) /mobius-yt" required data-validation-required-message="Please enter your CSE ID">
          <p class="help-block text-danger"></p>
        </div>
      </div>


      <!-- CSE NAME -->
      <div class="form-group row">
        <label class="col-sm-4">CSE NAME</label>
        <div class="col-sm-15">
          <input type="text" v-model="form.cse_name" class="form-control" id="cse_name" placeholder="ex) /mobius-yt" required data-validation-required-message="Please enter your CSE NAME">
          <p class="help-block text-danger"></p>
        </div>
      </div>

      <!-- CSE HOST -->
      <div class="form-group row">
        <label class="col-sm-4">CSE HOST</label>
        <div class="col-sm-15">
          <input type="text" v-model="form.cse_host" class="form-control" id="cse_host" placeholder="ex) 192.168.0.1" required data-validation-required-message="Please enter your CSE HOST">
          <p class="help-block text-danger"></p>
        </div>
      </div>

      <!-- CSE PORT -->
      <div class="form-group row">
        <label class="col-sm-4">CSE PORT</label>
        <div class="col-sm-15">
          <input type="text" v-model="form.cse_port" class="form-control" id="cse_port" placeholder="ex) 7579" required data-validation-required-message="Please enter your CSE PORT">
          <p class="help-block text-danger"></p>
        </div>
      </div>


      <!-- CSE MQTT PORT -->
      <div class="form-group row">
        <label class="col-sm-4">CSE MQTT PORT</label>
        <div class="col-sm-15">
          <input type="text" v-model="form.cse_mqtt_port" class="form-control" id="cse_mqtt_port" placeholder="ex) 1883" required data-validation-required-message="Please enter your CSE MQTT PORT">
          <p class="help-block text-danger"></p>
        </div>
      </div>
      <br>

      <!-- btn -->
      <div>
        <button type="submit" id="btnModify" class="btn btn-secondary btn-lg btn-block">Modify</button>
      </div>

    </form>
  </div>
</div>
</template>

<script>
export default {
  data: () => ({
    form : {
      name: "",
      node_id: "",
      hcl : "",
      cse_id : "",
      cse_host: "",
      cse_port: "",
      cse_mqtt_port: ""
    }
  }),
  methods: {
    clickEvent() {
    alert(JSON.stringify(this.form));
  



    } // 여기까지
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#title {
  font-style: italic;
  font-weight: bold;
  text-decoration: underline;

}

#form div {
  margin-bottom: 0px;

}

#form div label {
  font-style: italic;
  font-weight: bold;


}
form {
    width: 100%;
}

.btnModify {
  font-weight: bold;
}


</style>
