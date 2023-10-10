<script lang="ts">
    import { onMount } from "svelte";

    export let params;
    let foto;
    let imageURL;
    let title;
    let description;
    let deleteWarning: boolean = false;
    let edit: boolean = false;
    
    let titleRef;
    let descriptionRef;
    let lastTitle: string;
    let lastDescription: string;
    
    function enableEdit() {
        lastTitle = titleRef.innerHTML;
        lastDescription = descriptionRef.innerHTML;
        titleRef.style.border = "1px solid white";
        descriptionRef.style.border = "1px solid white";
        edit = true;
    }
    
    function disableEdit() {
        titleRef.innerHTML = lastTitle;
        descriptionRef.innerHTML = lastDescription;
        titleRef.style.border = "";
        descriptionRef.style.border = "";
        edit = false;
    }
    
    async function editImage() {
        console.log(titleRef.innerHTML);
        const formData = new FormData();
        formData.append("title", titleRef.innerHTML);
        formData.append("description", description.innerHTML);
        let response = await fetch("http://localhost:3000/fotos/" + params.foto, {
        method: "PUT",
        credentials: "include",
        headers: {
            "Content-Type": "application/json",
        },
        body: JSON.stringify({
            title: titleRef.innerHTML,
            description: descriptionRef.innerHTML
        })
       });
    }

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

{#if deleteWarning}
<div class="deleteModal">
    <div class="delete">
        Are you sure you want to delete this foto?
        <button on:click={deleteImage}>Delete</button> <button on:click={() => {deleteWarning = false}}>No</button>
    </div>
</div>
{/if}

<div class="content">
    <div class="foto">
        <h1 hidden>{title}</h1>
        <div class="imageContainer"><img src={imageURL || ""} alt="Uploaded"></div>
        <h2 bind:this={titleRef} contenteditable={edit ? "true": "false"}>{title}</h2>
        <p bind:this={descriptionRef} contenteditable={edit ? "true": "false"}>{description}</p>
        <div class="buttons">
            <div class="mode"><button on:click={enableEdit}>Edit</button><button on:click={() => {deleteWarning = true}}>Delete</button></div>
            {#if edit}
                <div class="confirm"><button on:click={disableEdit}>Cancel</button><button on:click={editImage}>Save</button></div>
            {/if}
        </div>
    </div>
</div>

<style>
    h1 {
        font-size: 10px;
    }
    .deleteModal {
        height: 100%;
        width: 100%;
        position: absolute;
        
        display: flex;
        justify-content: center;
        align-items: center;
        backdrop-filter: blur(5px); 
    }

    .content {
        height: calc(100vh - 60px);
        grid-column: span 12;
        display: flex;
        
        justify-content: center;
        align-items: center;
    }
    
    .foto {
        height: 80%;
        width: 80%;
        
        display: flex;
        flex-direction: column;
        justify-content: center;
    }
    
    .imageContainer {
        height: 450px;
        width: 800px;
        
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 0 auto 0 auto;
    }

    img {
        width: 60%;
        height: auto;
    }
    
    .buttons {
        display: flex;
        justify-content: space-between;
    }
</style>