<template>
    <div class="block">
      <div v-if="!hasSubmitted">
        <div class="choose_file">
          <input type="file" accept="image/*" @change="handleFileUpload" />
        </div>
        <div class="button">
          <button @click="submit" :disabled="!selectedFile || isUploading" class="submit-btn">
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
  
  <style scoped>
  .block {
    width: 100%;
    height: auto;
    border-radius: 10px;
    background: #eaeff0;
    color: black;
    text-align: center;
    padding: 30px;
    margin: 40px auto;
  }
  
  .choose_file input[type="file"] {
    padding: 8px 12px;
    border: 2px solid #3498db;
    border-radius: 5px;
    background-color: white;
    font-size: 16px;
    color: #2c3e50;
    cursor: pointer;
    transition: border-color 0.3s ease;
  }
  
  .choose_file input[type="file"]:hover {
    border-color: #2980b9;
  }
  
  .button {
    margin-top: 20px;
  }
  
  .submit-btn {
    padding: 12px 25px;
    font-size: 16px;
    background-color: #3498db;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .submit-btn:disabled {
    background-color: #bdc3c7;
    cursor: not-allowed;
  }
  
  .submit-btn:hover {
    background-color: #2980b9;
  }
  </style>
  