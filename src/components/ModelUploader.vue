<template>
  <v-app>
    <br><br><br><br>
    <v-container class="ma-24">
      <v-row align="center" justify="center" >
        <div  class="mb-5 font-weight-bold">
          EBM Model Uploader
        </div>
      </v-row>
       
      <v-form v-on:submit.prevent="submit">
          <!--<v-col cols="12" md="6" class="pl-sm-6">-->
            <br><br>
            <v-text-field v-model="model_data.name" label="name your model"></v-text-field>
            <v-file-input v-model="model_data.data" accept="zip, .zip, trt.pb, .trt.pb" label="upload your custom model" ></v-file-input>
            <v-file-input v-model="model_data.config" accept="application/json" label="upload config file" ></v-file-input>
            <v-btn class="blue rounded-pill" @click="submit">upload</v-btn>   
          <!--</v-col>-->
      </v-form>
      <br><br>
      <v-alert
          v-if="response"
          outlined
          :type="alertType"
          text
        >
          Upload successful ...
      </v-alert>

      <v-overlay v-model="overlay">
        <v-progress-circular
          indeterminate
          color="primary">
        </v-progress-circular>
      </v-overlay>
    </v-container>
    
  </v-app>
</template>

<script>
import axios from 'axios';

//import http_common from "@/services/http_common.js"
  export default {
    name: 'ModelUploader',
    
    data() {
      return {
        overlay:false,
        response:false,
        alertType:'success',
        model_data: {
          name:"",
          data: "",
          config: ""
        }
      }   
    }, 
    methods: {

      async submit() {
        let vm = this
      const config = {
        headers: { "content-type": "multipart/form-data" }
      };
      let formData = new FormData();
      for (let data in this.model_data) {
        formData.append(data, this.model_data[data]);
      }
      try {
        this.overlay =  true
        await axios.put('http://localhost:5000/admin/model/'+ encodeURIComponent(this.model_data.name), formData, config);
        console.log("model uploaded to AIAA")
        this.overlay = false
        this.alertType = 'success'
        this.response = true
        this.model_data.name =""
        this.model_data.data = ""
        this.model_data.config =""
        setTimeout(() =>{
          vm.response = false
        },3000)
        /*this.$router.push("/new"); */
      } catch (e) {
        this.overlay = false
        this.alertType = 'error'
        this.response = true
        setTimeout(() =>{
          vm.response = false
        },3000)
        console.log(e);
      }
      
    }
    },
    
  };






  //class="mx-12 my-8"
  /*
  methods: {
      onPick(){
        this.$refs.fileInput.click()
      },
      onFileChange(e) {
        let files = e.target.files || e.dataTransfer.files;
        if (files) {
          const fileReader = new FileReader()
          fileReader.onload = (e) => {
            this.imageData = e.target.result;
          }
          fileReader.readAsDataURL(files[0]);
          console.log(files[0]);
          this.model_data.model_file = files[0];
          console.log(this.model_data);
        }
      },
      async submit() {
        const config = {
          headers: {"content-type":"multipart/form-data"}
        };
        let formData = new FormData();
        for (let data in this.artist.data) {
          
        }
      }
    }

  htmls---------------------
  <!--
          <v-form v-on:submit.prevent="submit">
            <br>
            <br>
            <div class = "form-group">
              <v-text-field @click="onPick" label="upload your custom AI model"></v-text-field>
              <input 
              type="file"
              name = "model_file"
              style="display:none"
              ref="fileInput"
              accept=".zip,zip"
              required
              @change="onFileChange">
            </div>
            <div class = "form-group">
              <v-text-field @click="onPick" label="upload config file"></v-text-field>
              <input 
              type="file"
              name = "config_file"
              style="display:none"
              ref="fileInput"
              accept="application/json"
              required
              @change="onFileChange">
            </div>
            <v-btn class="blue rounded-pill" @click="submit">upload</v-btn> 
              
          </v-form>
          -->

    <!--<v-row>-->
        <!--<v-col cols="12" md="6" class="pl-sm-6">
          <div align="left" justify="center" >           
            <img src="@/assets/model.png" width=100% alt="EBM Model Uploader">
          </div>
        </v-col>--> 
  */
</script>
