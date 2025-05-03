<template>
    <div class="processing-wrapper">
      <div class="processing-container">
        <div class="image-section">
          <img :src="imageUrl" alt="Uploaded" class="preview-image" />
          <p class="section-label">Original Image</p>
        </div>
        <div class="result-section">
          <div class="spinner"></div>
          <p class="section-label">Processing...</p>
        </div>
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
  
  <style>
  .processing-wrapper {
    width: 100%;
    max-width: 1400px; /* Increased from 1200 */
    height: auto;
    display: flex;
    justify-content: center;
    margin: 0 auto; /* Changed from 0 */
    padding: 20px 0; /* Added padding */
  }
  
  .processing-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 30px;
    width: 100%;
    height: auto;
    border-radius: 10px;
    gap: 60px; /* Increased gap */
  }
  
  .image-section {
    flex: 1.2; /* Increased flex ratio */
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  
  .result-section {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  
  .preview-image {
    width: 100%;
    max-width: 500px; /* Increased max-width */
    height: auto;
    object-fit: contain;
    border-radius: 10px;
    margin-bottom: 15px; /* Increased margin */
  }
  
  .section-label {
    font-size: 32px;
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    color: rgb(7, 7, 7);
    margin-top: 12px; /* Increased margin */
    text-align: center;
    padding: 8px 20px; /* Increased padding */
    border-radius: 4px;
  }
  
  .spinner {
    border: 6px solid #82b0f1; /* Thicker border */
    border-top: 6px solid #1652a6; /* Thicker border */
    border-radius: 50%;
    width: 70px; /* Larger spinner */
    height: 70px; /* Larger spinner */
    animation: spin 1s linear infinite;
    margin-bottom: 15px; /* Increased margin */
  }
  
  @keyframes spin {
    to {
      transform: rotate(360deg);
    }
  }
  
  @media (max-width: 768px) {
    .processing-container {
      flex-direction: column;
      gap: 30px;
      padding: 30px 20px;
    }
    
    .image-section, .result-section {
      width: 100%;
    }
    
    .preview-image {
      max-width: 100%;
    }
  }
  </style>