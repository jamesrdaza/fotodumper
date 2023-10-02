<script lang="ts">
  import router from "page"
  import Home from "./routes/Home.svelte"
  import Profile from "./routes/Profile.svelte"
  import Login from "./routes/Login.svelte";
  import Foto from "./routes/Foto.svelte";
  import type { ComponentType } from "svelte";
  
  let page: ComponentType; 
  let params;

  router("/", (ctx, next) => { params = {}; next(); }, () =>(page = Home));
  router("/profile", (ctx, next) => { params = {}; next(); }, () => (page = Login));
  router("/profile/:user", (ctx, next) => { params = ctx.params; next(); }, () => (page = Profile));
  router("/fotos/:foto", (ctx, next) => { params = ctx.params; next(); }, () => (page = Foto))
  
  router.start();
</script>

<svelte:component this="{page}" {params}/>