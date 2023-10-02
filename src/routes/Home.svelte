<script lang="ts">
  import Navbar from "../components/Navbar.svelte"
  import { onMount } from "svelte"; 
  
  // Element References
  let image: HTMLImageElement;
  let imageFile: HTMLInputElement;

  function changePreviewSource() {
    const [file] = imageFile.files;
    if(file) {
      image.src = URL.createObjectURL(file);
    }
  }

  const submitImage = async (e) => {
    e.preventDefault();
    const formData = new FormData();
    formData.append("image", imageFile.files[0])

    await fetch("http://localhost:3000/fotos", {
      method: "POST",
      credentials: "include",
      body: formData
    });
  }

  // Declare Type Later
  let resJson: any;

  onMount(async () => {
    let test = await fetch("http://localhost:3000/user", {
      credentials: "include"
    });
    resJson = await test.json();
    console.log(resJson.name);
  })
</script>

<main>
  <Navbar username={resJson ? resJson.name : "Profile"}/>
  <div class="content">
    <div class="upload">
      <form on:submit={submitImage} >
        <input type="file" id="image" accept="image/png, image/jpeg" bind:this={imageFile} on:change={changePreviewSource}>
        <button id="UploadButton" type="submit">Upload an Image</button>
        <img src="#" alt="preview" bind:this={image}>
      </form>
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
