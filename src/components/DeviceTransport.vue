<template >
  <div class="container">
    <!-- header -->
    <div class="head">
        <br>
        <span id="title"><i class="fas fa-cog"></i>Device Transport Setting.</span>
    </div>
        <br><br>
    <!-- body -->
    <div class="body">
      <div class="mainTable">
          <table class="table">
              <thead>
                <tr>
                    <th>ID</th>
                    <th>Transport Name</th>
                    <th>Transport Type</th>
                    <th>Connection Info</th>
                    <th>Created At</th>
                    <th>Updated At</th>
                    <th>Management</th>
                </tr>
              </thead>
              <tbody>
                <!-- JSON data 순회하며 출력 : 동적으로 받아오기-->
                <!-- <tr v-for="(value, key, index) in models" :key="value.id">
                  <td>{{index}}</td>
                  <td>{{value.TransportName}}</td>
                  <td>{{value.TransportType}}</td>
                  <td>{{value.ConnectionInfo}}</td>
                  <td>{{value.CreatedAt}}</td>
                  <td>{{value.UpdatedAt}}</td> -->

                  <!-- test를 위해 정적으로 data 입력 -->
                <tr>
                  <td>{{1}}</td>
                  <td>{{1}}</td>
                  <td>{{1}}</td>
                  <td>{{1}}</td>
                  <td>{{1}}</td>
                  <td>{{1}}</td>

                  <!-- Management : edit / delete 버튼 -->
                  <td>
                      <button id="show-modal" class="btn btn-secondary edit-btn" @click="showModal = true, plus()">
                          EDIT</i>
                      </button>
                      <button class="remove-btn btn btn-secondary" id="show-modal-edit" v-on:click="remove()">
                        DEL</i>
                      </button>
                  </td>
              </tr>
              <br>
              </tbody>
            </table>
          </div>

              <!-- +(ADD) 버튼 클릭시 상세정보 입력창으로 이동 -->
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
                            <b-form id="form" @submit="onSubmit">

                                <!-- Transport Name -->
                                    <b-form-group label="Transport Name">
                                      <b-form-select :options="TransportType"
                                        required v-model="model.TransportName">
                                      </b-form-select>
                                    </b-form-group>

                                  <!-- Transport Type -->
                                  <b-form-group label="Transport Type">
                                      <b-form-input type="text" v-model="model.TransportType"
                                        required placeholder="ex) /mobius-yt">
                                      </b-form-input>
                                  </b-form-group>

                                  <!-- Connection Info -->
                                  <b-form-group label="Connection Info">
                                      <b-form-input type="text" v-model="model.ConnectionInfo"
                                        required placeholder='ex) {"type":"tcp", "host":"192.168.0.1", "port":502}'>
                                      </b-form-input>
                                  </b-form-group>
                                  <!-- footer 버튼 부분 -->
                                  <div class="modal-footer">
                                    <slot name="footer">
                                      <!-- SAVE / CANCEL 버튼 -->
                                      <button class="ok-btn modal-default-button btn btn-secondary" type="submit" mode = 'save'>
                                          Save
                                      </button>
                                      <button class="cancel-btn modal-default-button btn btn-secondary" type="button" @click="mode = 'list'" >
                                          Cancel
                                      </button>
                                    </slot>
                                  </div><!--footer-->
                              </b-form>
                            </slot>
                          </div><!--body-->
                        </div>

                        </div>
                      </div>
                    </transition>
                  </template> <!--modal-->
                </div>


          </div><!--second depth-->

      <!-- ADD버튼 -->
      <button id="show-modal" class="btn btn-secondary btn-add" @click="showModal = true, plus()"><i class="fas fa-plus"></i></button>
      <!-- use the modal component, pass in the prop -->
      <modal v-if="showModal" @close="showModal = false"></modal>

      </modal>

    </div><!--body-->
  </div>
</template>

<script>



export default {
  name: 'Table',
  props: {
    msg: String,
    changeList : Function
  },
  // 모델 생성
  data () {
    return {
      showModal: false,
      //  상태값 구분 위한 mode
      mode:'list',
      //  예시모델 id
      model : {
        id:'',
        TransportName : '',
        TransportType : '',
        ConnectionInfo : '',
        CreatedAt : '',
        UpdatedAt : '',
        Management : '',
      },
      // 값을 저장할 배열
      models: [],
      TransportType: [
        { text : "Select Transport Type", value:null},
        'IP', 'RTU'
      ],
      show:true
    }
  },
  //  메서드
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      var id = this.models.length + 1;
      //  저장 클릭시 내용 저장
      //  mode가 save이면 내용 저장
      if(this.mode === 'save') {
        this.models.push({
          // JSON
          id:id,
          TransportName : this.model.TransportName,
          TransportType : this.model.TransportType,
          ConnectionInfo : this.model.ConnectionInfo,
          CreatedAt : new Date(),
          UpdatedAt : new Date()
        });
      } else if(this.mode === 'edit'){
        for(var i in this.models) {
          if(this.models[i].id === this.model.id){
            this.models[i] = this.renew(this.model);
            break;
          }
        }
      }

      //  저장하고나서는 상태값 list로 변경
      this.mode = 'list';
      // console 확인용 내부저장소 이용
      localStorage.setItem('models', JSON.stringify(this.models));
      alert(JSON.stringify(this.model));
    },
    renew :  function(val) {
      return JSON.parse(JSON.stringify(val))
    },
    // +버튼 클릭시 모달창
    plus: function(){
      this.mode = 'plus'
      /* this.model ={
        //  빈값으로 초기화
        id:this.model.id,
        TransportName : null,
        TransportType : null,
        ConnectionInfo : null,
        CreatedAt : new Date(),
        UpdatedAt : new Date()
      } */
    },
    remove : function() {
      if(confirm('Are you sure want to delete?')){
        for(var i in this.models) {
          if(this.models[i].id === this.model.id) {
            this.models.splice(i, 1);
            break;
          }
        }
        this.mode = 'list';
        localStorage.setItem('models', JSON.stringify(this.models))
      }
    },
  },
  // 시작될 때 제일 먼저 구동됨(data 유지)
  created: function() {
    var models = localStorage.getItem('models');
    if(models) {
      this.models = JSON.parse(models);
    }
  },
  computed: {
    showList() {
      return this.models;
    }
  }
}
</script>




<style>
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
