<template>
  <div class="upload-file">
    <label
      >ファイルアップロード
      <input
        class="button--grey"
        type="file"
        id="file"
        ref="file"
        v-on:change="handleFileUpload()"
      />
    </label>
    <button v-on:click="submitFile()" class="button--grey">SUBMIT</button>
  </div>
</template>

<script>
import axios from "axios";
  export default {

    data(){
      return {
        file: ''
      }
    },

    methods: {
      submitFile(){

            let formData = new FormData();

            formData.append('file', this.file);

            axios.post( '/single-file',
                formData,
                {
                headers: {
                    'Content-Type': 'multipart/form-data'
                }
              }
            ).then(function(){
          console.log('SUCCESS!!');
        })
        .catch(function(){
          console.log('FAILURE!!');
        });
      },

      handleFileUpload(){
        this.file = this.$refs.file.files[0];
      }
    }
  }
</script>

<style>
.upload-file{
    margin-top: 5%;
}
</style>