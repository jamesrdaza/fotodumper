<script>
    import { onMount } from "svelte";

    export let params;
    let foto;
    let imageURL;
    let title;
    let description;
    
    async function deleteImage() {
        console.log("DETLETING");
        let response =  await fetch("http://localhost:3000/fotos/" + params.foto, {
             method: "DELETE",
             credentials: "include"
        });
        if (response.status === 200) {
            window.location.replace("http://localhost:5173/");
        }
    }

    onMount(async () => {
        let response = await fetch("http://localhost:3000/fotos/" + params.foto, {
            credentials: "include"
        });
        foto = await response.json();
        imageURL = foto.imageURL;
        title = foto.title;
        description = foto.description;
    });
    
</script>

<img src={imageURL || ""} alt="">
<h1>{title}</h1>
<p>{description}</p>
<button on:click={deleteImage}>Delete</button>