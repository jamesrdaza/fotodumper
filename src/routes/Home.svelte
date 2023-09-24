<script lang="ts">
  import Navbar from "../components/Navbar.svelte"
  import { onMount } from "svelte"; 

  let resJson;
  onMount(async () => {
    let test = await fetch("http://localhost:3000/testLogin", {
      credentials: "include"
    });
    resJson = await test.json();
    console.log(resJson.name);
  })
</script>

<main>
  <Navbar username={resJson ? resJson.name : "test"}/>
  <div class="content">
    <div class="upload">
      <button id="UploadButton">Upload an Image</button>
    </div>
  </div>
</main>

<style>
  main {
    min-height: 100vh;
    width: 100%;
    display: grid;
    grid-template-columns: repeat(12, 1fr);
  }
  
  .content {
    height: calc(100vh - 60px);
    grid-column: span 12;
    
    display: flex;
  }
  
  .upload {
    height: 35%;
    width: 100%;
    display: flex;
    
    justify-content: center;
    align-items: center;
  }
  
  #UploadButton {
   height: 30px; 
  }
</style>
