<script lang="ts">
  import Navbar from "../components/Navbar.svelte"
  import { onMount } from "svelte"; 
  
  // Element References
  let image: HTMLImageElement;
  let imageFile: HTMLInputElement;
  let title: HTMLInputElement;
  let description: HTMLInputElement;

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

</script>

<div class="content">
  <div class="upload">
    <form on:submit={submitImage} >
      <input type="file" id="image" accept="image/png, image/jpeg" bind:this={imageFile} on:change={changePreviewSource}>
      <label for="title">Title</label>
      <input type="text" name="title" bind:this={title}>
      <label for="description">Description</label>
      <input type="text" name="description" bind:this={description}>
      <button id="UploadButton" type="submit">Upload an Image</button>
      <img src="#" alt="preview" bind:this={image}>
    </form>
  </div>
</div>

<style>
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
  
  form {
    
  }
  
  #UploadButton {
   height: 30px; 
  }
</style>
