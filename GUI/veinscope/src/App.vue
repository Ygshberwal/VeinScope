<template>
  <div id="app">
    <HeaderComponent />


    <!-- If using Vue Router -->
    <router-view v-if="!isUploading" />

    <!-- Or directly rendering UploadBody -->
    <UploadBody v-if="isUploading" />
  </div>
</template>

<script>
import UploadBody from './components/UploadBody.vue';
import HeaderComponent from './components/HeaderComponent.vue';

export default {
  name: 'App',
  components: {
    UploadBody,
    HeaderComponent,
  },
  data() {
    return {
      isUploading: true,
    };
  },
};
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

h1 {
  margin-top: 20px;
  font-size: 28px;
  color: #2c3e50;
}
</style>
