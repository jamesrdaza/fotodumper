<script>
    import { onMount } from "svelte";
    
    export let params;
    
    let fotosArray = [];
    
    onMount(async () => {
        let fotos = await fetch("http://localhost:3000/fotos", {
            credentials: "include"
        });
        fotosArray = await fotos.json();
    });
</script>

<div class="content">
    {params.user}'s Fotos
    <div class="fotos">
        {#each fotosArray as foto}
            <div class="foto">
                <a href={"/fotos/" + foto.image_name}><img src={foto.imageURL} alt="foto"></a>
            </div>
        {/each}
    </div>
</div>

<style>
    .content {
        height: calc(100vh - 60px);
        grid-column: span 12;
    }
    
    .fotos {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
    }
    
    a {
        height: 250px;
        width: 400px;
        
        display: flex;
        justify-content: center;
        align-items: center;
    }
    
    img {
        width: 60%;
        height: auto;
    }
</style>
