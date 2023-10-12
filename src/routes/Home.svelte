<script lang="ts">
  import { onMount } from "svelte"; 
  
  // Element References
  let image: HTMLImageElement;
  let imageFile: HTMLInputElement;
  let title: HTMLInputElement;
  let description: HTMLTextAreaElement;
  let preview: HTMLDivElement;
  let upload: HTMLDivElement;
  let uploadButton: HTMLLabelElement;
  let form: HTMLFormElement;

  let show: boolean = false;

  function changePreviewSource() {
    show = true; // Set show flag to true to render the rest of the form

    // Manipulate Element styles for animation
    preview.style.height = "90%";
    preview.style.width = "75%";
    upload.style.flex = "0 0 auto";
    uploadButton.style.width = "95%";
    form.style.height = "100%";
    form.style.width = "100%";
    
    // Load uploaded file as source of preview image
    const [file] = imageFile.files;
    if(file) {
      image.src = URL.createObjectURL(file);
    }
  }

  const submitImage = async (e) => {
    e.preventDefault(); // Prevent page reloading

    // Create form object
    const formData = new FormData();
    formData.append("image", imageFile.files[0])
    formData.append("title", title.value);
    formData.append("description", description.value);

    // Send POST request to API to upload image
    let response = await fetch("http://localhost:3000/fotos", {
      method: "POST",
      credentials: "include",
      body: formData
    });
    
    // Redirect to image upon successful upload
    if (response.status === 200) {
     console.log(response.status); 
      let responseJson = await response.json();
      console.log(responseJson);
      window.location.replace("http://localhost:5173/fotos/" + responseJson.imageName);
    }
  }

  // Declare Type Later
  let resJson: any;

  // Load user info
  onMount(async () => {
    let test = await fetch("http://localhost:3000/user", {
      credentials: "include"
    });
    resJson = await test.json();
  })
</script>

<div class="content">
  <div class="upload" bind:this={upload}>
    <form on:submit={submitImage} bind:this={form}>
      <label for="image" bind:this={uploadButton}>
        Upload File
      </label>
      <input type="file" id="image" name="fileImage" accept="image/png, image/jpeg" bind:this={imageFile} on:change={changePreviewSource} style="display: none">
      {#if show}
        <div class="textSubmit">
          <input type="text" name="title" placeholder="Title" bind:this={title}>
        </div>
        <div class="textSubmit">
          <textarea name="description" id="description" cols="22" rows="10" bind:this={description} placeholder="Enter a description..." style="resize: none"></textarea>
        </div>
        <button id="UploadButton" type="submit">Upload</button>
      {/if}
    </form>
  </div>
  <div class="preview" bind:this={preview}>
    <img src="data:image/gif;base64,R0lGODlhAQABAAD/ACwAAAAAAQABAAACADs%3D" alt="preview" bind:this={image}>
  </div>
</div>

<style>
  .content {
    height: calc(100vh - 60px);
    grid-column: span 12;
    
    display: flex;
    flex-flow: row;
    justify-content: space-evenly;
    align-items: center;
  }
  
  .upload {
    height: 90%;
    width: 20%;
    display: flex;
    
    justify-content: center;
    align-items: center;
    
    margin: 0;
    flex: 1 0 auto;
  }
  
  form {
    height: 40%;
    width: 30%;

    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;

    background-color: #2D2D2B;
    box-shadow: 0 0 41px 4px rgba(18, 18, 18, 0.5);
    border-radius: 5px;
    transition: 0.25s;
  }

  .textSubmit {
    width: 100%;
    display: flex;

    justify-content: center;
    align-items: center;
  }
  
  textarea {
    width: 93%;
    margin-top: 10px;
  }
  
  label {
    float: left;
    width: 100%;
  }

  label[for="image"] {
    width: 30%;
    height: 40px;
    margin-right: 0;
    border-radius: 5px;

    line-height: 40px;
    cursor: pointer;

    text-align: center;
    background-color: green;
  }
  
  #UploadButton {
   height: 30px; 
   line-height: 30px;
  }
  
  
  input[type="text"] {
    height: 35px;
    width: 95%;
    margin-top: 10px;
    box-sizing: border-box;
    font-size: 20px;
  }
  
  input:focus, textarea:focus {
    outline: none;
  }
  
  button {
    margin-top: 10px;
    width: 95%;
    border-radius: 5px;
    height: 40px;
  }
  
  .preview {
    width: 0;
    height: 0;
    margin: 0; 
    
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: black;
    box-shadow: 0 0 41px 4px rgba(18, 18, 18, 0.5);
    
    transition: 0.25s;
    border-radius: 5px;
  }
  
  img {
    max-height: 100%;
    max-width: 80%;
  }
</style>
