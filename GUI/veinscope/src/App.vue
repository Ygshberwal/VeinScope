<template>
  <h1> Vein Scope</h1>
  <!-- <button @click="upload">Upload Eye Image</button> -->
  <UploadBody v-if="isUploading">
  </UploadBody>
</template>

<script>
import UploadBody from './components/UploadBody.vue'     //Importing default export of Body.vue

export default {
  name: 'App',
  components: { UploadBody },
  data(){
    return{
      isUploading: true,

    }
  },
  methods:{
    upload(){

    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}
</style>

