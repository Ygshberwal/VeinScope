<template>
    <header class="app-header">
      <h1>Vein Scope</h1>
      <nav>
        <a href="#">Home</a>
        <a href="#">Upload</a>
        <a href="#">About</a>
      </nav>
    </header>
  </template>
  
  <script>
  export default {
    name: 'HeaderComponent',
  };
  </script>
  
  <style scoped>
  .app-header {
    background-color: #3b6b9a;
    color: white;
    border-radius: 10px;
    padding: 15px 30px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 4px solid #3498db;
  }
  
  .app-header h1 {
    margin: 0;
    font-size: 24px;
    color: aliceblue;
  }
  
  nav a {
    margin-left: 20px;
    color: white;
    text-decoration: none;
    font-weight: bold;
  }
  
  nav a:hover {
    text-decoration: underline;
  }
  </style>
  