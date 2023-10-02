<script>
    import { onMount } from "svelte";

    export let params;

    const getId = async() => {
        console.log(params.user)
    };
    
    let fotosArray = [];
    
    onMount(async () => {
        let fotos = await fetch("http://localhost:3000/fotos", {
            credentials: "include"
        });
        fotosArray = await fotos.json();
    });
</script>
Profile

{#each fotosArray as foto}
    <a href={"/fotos/" + foto.image_name}><img src={foto.imageURL} alt="foto"></a>
{/each}
