<script>
    import { onMount } from "svelte";

    export let params;

    const getId = async() => {
        console.log(params.user)
    };
    
    onMount(() => getId());
</script>
Profile