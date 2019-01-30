<template lang="html">
  <div class="">
    <div class="">
      <table class ="table"  >
        <th colspan="5">Resource Device</th>
        <tr>
          <th>index</th>
          <th>id</th>
          <th>password</th>
          <th>name</th>
          <th>util</th>
        </tr>
        <tr v-for="(test, key, index) in form">
          <td>{{index+1}}</td>
          <td>{{test.id}}</td>
          <td>
            {{test.password}}
          </td>
          <td>
            {{test.name}}
          </td>
          <td>
              <button @click="deleteEvent(test)" type="button" name="button">delete</button>
              <button @click="updateEvent(test)" type="button" name="button">update</button>
                <div class="second-depth" v-if="mode ==='plus'">
                  <template id="modal-template">
                    <!-- modal -->
                    <transition name="modal">
                      <div class="modal-mask">
                        <div class="modal-wrapper">
                          <div class="modal-container">
                            <!-- header -->
                            <div class="modal-header">
                                <h3 slot="header"><i class="fas fa-plus"></i>Add Device</h3>
                            </div>
                            <!-- body -->
                            <div class="modal-body">
                              <slot name="body">
                              <!-- body 폼입력 부분 -->
                              <b-form id="form" @submit="updateTest(test)">
                                <div >
                                  바꿀페스워드를 입력해주새요
                                </div>
                                <input v-model="update.password" type="password" placeholder="password">
                                  <!-- footer 버튼 부분 -->
                                    <div class="modal-footer">
                                      <slot name="footer">
                                        <!-- SAVE / CANCEL 버튼 -->
                                        <button class="ok-btn modal-default-button btn btn-secondary" type="submit">
                                            Save
                                        </button>
                                        <button class="cancel-btn modal-default-button btn btn-secondary" type="button" @click="mode = 'list'" >
                                            Cancel
                                        </button>
                                      </slot>
                                    </div><!--footer -->
                                </b-form>
                              </slot>
                            </div><!--body-->
                          </div>

                          </div>
                        </div>
                      </transition>
                    </template> <!--modal-->
                  </div>
          </td>
        </tr>
        <tr>
          <td  colspan="4">
            <input v-model="inform.password" type="text" placeholder="Password">
            <input v-model="inform.name" type="text" placeholder="Name">
            <button @click="clickEvent" type="button" name="button">save</button>
          </td>
        </tr>
      </table>

    </div>
    <pre>
      <div style="text-align: left;">
        {{$data}}
      </div>
    </pre>
  </div>
</template>

<script>
var name;
export default {
  data() {
    return {
      form: [],
      inform: {},
      update: {},
      mode: ''
    }
  },
  mounted: function() {
    this.fetchEvent()
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      /* this.form.push(this.form); */
    },
    clickEvent() {
      console.log('click');
      axios.post('http://192.168.10.103:3000/addUser/' + this.inform.name, {
          password: this.inform.password,
          name: this.inform.name
        })
        .then(response => {
          console.log(response);
          this.fetchEvent()
        })
        .catch(response => {
          console.log(response);
          console.log("error");
        });
    },
    fetchEvent() {
      var vm = this;
      axios.get('http://192.168.10.103:3000/list')
        .then(function(response) {
          console.log(response.data);
          vm.form = response.data;
        })
    },
    deleteEvent(test) {
      console.log(test.name);
      axios.delete('http://192.168.10.103:3000/deleteUser/' + test.name)
        .then(response => {
          this.fetchEvent()
        })
    },
    updateEvent(test) {
      console.log(test.name);
      name = test.name;
      this.mode = 'plus';
    },
    updateTest(test) {
      console.log('update');
      console.log(name);
      console.log(this.update.password);
      axios.put('http://192.168.10.103:3000/updateUser/' + name, {
          password: this.update.password,
          name: name
        })
        .then(response => {
          this.fetchEvent()
        })
      this.mode = 'list'
    }
  }

}
</script>

<style lang="css" scoped>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, .5);
  display: table;
  transition: opacity .3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 600px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
  transition: all .3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
  margin-top: 0;
  font-style: italic;
  font-weight: bold;
  text-decoration: underline;
  text-align: center;

}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
  font-style: italic;
  font-weight: bold;
}

/*
 * The following styles are auto-applied to elements with
 * transition="modal" when their visibility is toggled
 * by Vue.js.
 *
 * You can easily play with the modal transition by editing
 * these styles.
 */

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}

#title {
  font-style: italic;
  font-weight: bold;
  text-decoration: underline;
  font-size: x-large;
}

#form div {
    margin-bottom: 0px;
}


.b-form-group {
  font-style: italic;
  font-weight: bold;
  padding-right: 15px;
}

.edit-btn {
  margin-right: 5px;
}
</style>
