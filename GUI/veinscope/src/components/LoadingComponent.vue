<template>
    <div class="processing-container">
      <div class="image-section">
        <img :src="imageUrl" alt="Uploaded" class="preview-image" />
        <p>Original Image</p>
      </div>
      <div class="result-section">
        <div class="spinner"></div>
        <p>Processing...</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'LoadingComponent',
    props: {
      imageUrl: {
        type: String,
        required: true,
      },
    },
  };
  </script>
  
  <style scoped>
  .processing-container {
    display: flex;
    justify-content: space-around;
    align-items: center;
    padding: 20px;
    height: 250px;
    border-radius: 10px;
  }
  
  .image-section,
  .result-section {
    flex: 1;
    text-align: center;
  }
  
  .preview-image {
    width: 200px;
    height: 200px;
    object-fit: contain; /* Keeps image aspect ratio within bounds */
    border: 2px solid #ccc;
    border-radius: 10px;
    background-color: white;
  }
  
  .spinner {
    border: 5px solid #e0e0e0;
    border-top: 5px solid #3498db;
    border-radius: 50%;
    width: 40px;
    height: 40px;
    animation: spin 1s linear infinite;
    margin: 0 auto 10px;
  }
  
  @keyframes spin {
    to {
      transform: rotate(360deg);
    }
  }
  </style>
  