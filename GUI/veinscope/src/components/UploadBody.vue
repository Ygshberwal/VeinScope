<template>
    
    <div class="upload-container-wrapper">
        <!-- <div class="upload-container"> -->

      <div v-if="!hasSubmitted">
        <div 
          class="upload-area"
          @click="triggerFileInput"
        >
          <input 
            type="file" 
            ref="fileInput"
            accept="image/*" 
            @change="handleFileUpload" 
            class="hidden-input"
          />
          
          <div v-if="!uploadedImageUrl" class="upload-placeholder">
            <div class="upload-icon">
              <svg width="40" height="40" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M12 16V8M12 8L9 11M12 8L15 11" stroke="#9CA3AF" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
                <path d="M16 4H8C6.34315 4 5 5.34315 5 7V17C5 18.6569 6.34315 20 8 20H16C17.6569 20 19 18.6569 19 17V7C19 5.34315 17.6569 4 16 4Z" stroke="#9CA3AF" stroke-width="2"/>
              </svg>
            </div>
            <p class="upload-text">Click or tap to upload an image</p>
            <p class="upload-hint">(Supports JPG, PNG, GIF, etc.)</p>
          </div>
          
          <div v-else class="preview-container">
            <img :src="uploadedImageUrl" alt="Preview" class="image-preview" />
          </div>
        </div>
        
        <div class="button-container">
          <button 
            @click="submit" 
            :disabled="!selectedFile || isUploading" 
            class="submit-button"
            :class="{'button-disabled': !selectedFile || isUploading}"
          >
            {{ isUploading ? 'Uploading...' : 'Analyze Image' }}
          </button>
        </div>
      </div>
      
      <div v-else>
        <LoadingComponent :image-url="uploadedImageUrl" />
      </div>
      </div>
    <!-- </div> -->
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
      triggerFileInput() {
        this.$refs.fileInput.click();
      },
      handleFileUpload(event) {
        const file = event.target.files[0];
        if (file && file.type.startsWith('image/')) {
          this.selectedFile = file;
          this.uploadedImageUrl = URL.createObjectURL(file);
        } else if (file) {
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
  .upload-container-wrapper {
    max-width: 100%;
    /* width: 1500px; */
    margin: 40px auto;
    padding: 10px 30% 0 30%;
    
  }

  .upload-container {
    max-width: 40%;
    margin: 40px auto;
  }
  
  .upload-area {
    position: relative;
    height: auto;
    border: 2px dashed #cbd5e0;
    border-radius: 8px;
    background-color: #f8fafc;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: border-color 0.3s, background-color 0.3s;
    margin-bottom: 16px;
    overflow: hidden;
  }
  
  .upload-area:hover {
    border-color: #93c5fd;
    background-color: #f0f9ff;
  }
  
  .hidden-input {
    position: absolute;
    width: 0;
    height: 0;
    opacity: 0;
  }
  
  .upload-placeholder {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: #6b7280;
  }
  
  .upload-icon {
    margin-bottom: 10px;
  }
  
  .upload-text {
    font-size: 14px;
    font-weight: 500;
    margin-bottom: 4px;
    color: #4b5563;
  }
  
  .upload-hint {
    font-size: 12px;
    color: #9ca3af;
  }
  
  .preview-container {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 16px;
  }
  
  .image-preview {
    max-width: 100%;
    max-height: 100%;
    object-fit: contain;
  }
  
  .button-container {
    width: 100%;
  }
  
  .submit-button {
    width: 100%;
    padding: 12px;
    border-radius: 6px;
    font-size: 16px;
    font-weight: 500;
    background-color: #3b82f6;
    color: white;
    border: none;
    cursor: pointer;
    transition: background-color 0.2s;
  }
  
  .submit-button:hover:not(.button-disabled) {
    background-color: #2563eb;
  }
  
  .button-disabled {
    background-color: #93c5fd;
    cursor: not-allowed;
  }
  </style>