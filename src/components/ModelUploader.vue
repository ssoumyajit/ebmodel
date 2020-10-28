<template>
  <v-app>
    <br><br><br><br><br><br><br>
    <v-container class="ma-24">
      <v-row align="center" justify="center" >
        <div  class="mb-5 font-weight-bold">
          EBM Model Uploader
        </div>
      </v-row>
      <hr>
      <v-row>
        <v-col cols="12" md="6" class="pl-sm-6">
          <div align="left" justify="center" >           
            <v-img src="@/assets/model.png" width=100% alt="EBM Model Uploader"> </v-img>
          </div>
        </v-col>

        <v-col cols="12" md="6" class="pl-sm-6">
          <div>
            <br>
            <br>
            <v-file-input label="upload your custom AI model"></v-file-input>
            <v-file-input label="upload config file"></v-file-input>
          </div>
          
        </v-col>
      </v-row>
      
      
    </v-container>
    

  </v-app>
</template>

<script>
  export default {
    name: 'ModelUploader',

    data: () => ({}),
  }
  //class="mx-12 my-8"
</script>
