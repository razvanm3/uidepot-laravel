<template>
  <div class="modal-mask">
    <div class="modal-wrapper">
      <div class="container">
        <div class="row">
        <div class="col-md-6">
          <slot name="header" v-html="data.name"></slot>
          <slot name="body">
          <ul style="list-style-type:none">
            <li>Name: </li>
            <li><input type="text" v-model="data.name"></li>
            <li>Units: </li>
            <li><input type="text" v-model="data.units"></li>
            <li>Price: </li>
            <li><input type="text" v-model="data.price"></li>
            <li>Description: </li>
            <textarea v-model="data.description"></textarea>
            <img :src="data.image" v-show="data.image != null">
            <li><input type="file" id="file" @change="attachFile"></li>
            <p></p>
            <li><button class="button btn-primary" @click="uploadFile">Finish</button></li>
          </ul>
          </slot>
        </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  export default {
    props : ['product'],
    data(){
      return {
        attachment : null
      }
    },
    computed : {
      data : function(){
        if(this.product != null){
          return this.product
        }
        else {
          return {
            name : "", 
            units : "", 
            price : "",
            description : "",
            image : false

          }
        }
      }
    },
    methods : {
      attachFile(event){
        this.attachment = event.target.files[0];
      },
      uploadFile(event){
        if(this.attachment != null){
          var formData = new FormData();
          formData.append("image", this.attachment)
          axios.post("/api/upload-file", formData, {
            headers: {
              'Content-Type': 'multipart/form-data'
            }
          })
          .then(response => {
            this.product.image = response.data
            this.$emit('close', this.product)
          })
        }
        else {
          this.$emit('close', this.product)
        }
      }
    }
  }
</script>
<style scoped>
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
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
  transition: all .3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.container {
  background-color: #fff;
  padding: 10px 10px;
  border-radius: 2px;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
}

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
</style>