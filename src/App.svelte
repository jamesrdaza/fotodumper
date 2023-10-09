<script lang="ts">
  import router from "page"
  import Home from "./routes/Home.svelte"
  import Profile from "./routes/Profile.svelte"
  import Login from "./routes/Login.svelte";
  import Foto from "./routes/Foto.svelte";
  import Navbar from "./components/Navbar.svelte";
  import { onMount } from "svelte";
  import type { ComponentType } from "svelte";

  // Declare Type Later
  let resJson: any;

  onMount(async () => {
    let test = await fetch("http://localhost:3000/user", {
      credentials: "include"
    });
    resJson = await test.json();
  })
  
  let page: ComponentType; 
  let params = {};

  router("/", () =>(page = Home));
  router("/profile", () => (page = Login));
  router("/profile/:user", (ctx, next) => { params = ctx.params; next(); }, () => (page = Profile));
  router("/fotos/:foto", (ctx, next) => { params = ctx.params; next(); }, () => (page = Foto))
  
  router.start();
</script>

<main>
  <Navbar username={resJson ? resJson.name : "Profile"}/>
  <svelte:component this="{page}" {params}/>
</main>

<style>
  main {
    min-height: 100vh;
    width: 100%;
    display: grid;
    grid-template-columns: repeat(12, 1fr);
  }
</style>