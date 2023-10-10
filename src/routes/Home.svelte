<script lang="ts">
  import Navbar from "../components/Navbar.svelte"
  import { onMount } from "svelte"; 
  
  // Element References
  let image: HTMLImageElement;
  let imageFile: HTMLInputElement;
  let title: HTMLInputElement;
  let description: HTMLInputElement;

  let show: boolean = false;

  function changePreviewSource() {
    show = true;
    const [file] = imageFile.files;
    if(file) {
      image.src = URL.createObjectURL(file);
    }
  }

  const submitImage = async (e) => {
    e.preventDefault();

    const formData = new FormData();
    formData.append("image", imageFile.files[0])
    formData.append("title", title.value);
    formData.append("description", description.value);

    let response = await fetch("http://localhost:3000/fotos", {
      method: "POST",
      credentials: "include",
      body: formData
    });
    
    if (response.status === 200) {
     console.log(response.status); 
      let responseJson = await response.json();
      console.log(responseJson);
      window.location.replace("http://localhost:5173/fotos/" + responseJson.imageName);
    }
  }

  // Declare Type Later
  let resJson: any;

  onMount(async () => {
    let test = await fetch("http://localhost:3000/user", {
      credentials: "include"
    });
    resJson = await test.json();
  })
</script>

<div class="content">
  <div class="upload">
    <form on:submit={submitImage} >
      <input type="file" id="image" accept="image/png, image/jpeg" bind:this={imageFile} on:change={changePreviewSource}>
      {#if show}
        <div class="textSubmit">
          <label for="title">Title</label>
          <input type="text" name="title" bind:this={title}>
        </div>
        <div class="textSubmit">
          <label for="description">Description</label>
          <input type="text" name="description" bind:this={description}>
        </div>
        <button id="UploadButton" type="submit">Upload an Image</button>
      {/if}
      <img src="data:image/gif;base64,R0lGODlhAQABAAD/ACwAAAAAAQABAAACADs%3D" alt="preview" bind:this={image}>
    </form>
  </div>
</div>

<style>
  .content {
    height: calc(100vh - 60px);
    grid-column: span 12;
    
    display: flex;
    justify-content: center;
  }
  
  .upload {
    height: 65%;
    width: 35%;
    display: flex;
    margin-top: 10px;
    
    justify-content: center;
    align-items: center;
    
    border: 1px solid black;
    border-radius: 15px;
  }
  
  form {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }

  .textSubmit {
    width: 100%;
  }
  
  label {
    text-align: left;
    clear: both;
    margin-right: 10px;
    float: left;
    width: 25%;
  }
  
  #UploadButton {
   height: 30px; 
  }
</style>
