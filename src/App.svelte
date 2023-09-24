<script lang="ts">
  import router from "page"
  import Home from "./routes/Home.svelte"
  import Profile from "./routes/Profile.svelte"
  import Login from "./routes/Login.svelte";
  import type { ComponentType } from "svelte";
  
  let page: ComponentType; 
  let params;

  router("/", () => (page = Home));
  router("/profile", () => (page = Login));
  router("/profile/:user", (ctx, next) => { params = ctx.params; next(); }, () => (page = Profile));
  
  router.start();
</script>

<svelte:component this="{page}" {params}/>