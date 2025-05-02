<template>
    <div class="block">
      <div v-if="!hasSubmitted">
        <div class="choose_file">
          <input type="file" accept="image/*" @change="handleFileUpload" />
        </div>
        <div class="button">
          <button @click="submit" :disabled="!selectedFile || isUploading">
            {{ isUploading ? 'Uploading...' : 'Submit' }}
          </button>
        </div>
      </div>
      <div v-else>
        <LoadingComponent :image-url="uploadedImageUrl" />
      </div>
    </div>
  </template>
  
  <script>
  import LoadingComponent from './LoadingComponent.vue';
  
  export default {
    name: 'UploadBody',
    components: {
      LoadingComponent,
    },
    data() {
      return {
        isUploading: false,
        hasSubmitted: false,
        selectedFile: null,
        uploadedImageUrl: null,
      };
    },
    methods: {
      handleFileUpload(event) {
        const file = event.target.files[0];
        if (file && file.type.startsWith('image/')) {
          this.selectedFile = file;
          this.uploadedImageUrl = URL.createObjectURL(file);
        } else {
          alert('Only image files are allowed.');
          this.selectedFile = null;
          this.uploadedImageUrl = null;
        }
      },
      async submit() {
        if (!this.selectedFile) return;
        this.isUploading = true;
  
        const formData = new FormData();
        formData.append('file', this.selectedFile);
  
        try {
          // Simulate backend call delay
          await new Promise(resolve => setTimeout(resolve, 2000));
  
          // Replace this with your actual upload call
          // await fetch('/upload', { method: 'POST', body: formData });
  
          this.hasSubmitted = true;
        } catch (error) {
          console.error('Upload failed:', error);
          alert('Upload failed. Please try again.');
        } finally {
          this.isUploading = false;
        }
      },
    },
  };
  </script>
  