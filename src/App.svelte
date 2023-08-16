<script lang="ts">
  import router from "page"
  import Home from "./routes/Home.svelte"
  import Profile from "./routes/Profile.svelte"
  import type { ComponentType } from "svelte";
  
  let page: ComponentType; 
  let params: ComponentType;

  router("/", () => (page = Home));
  router("/profile", () => (page = Profile));
  
  router.start();
</script>

<svelte:component this="{page}" />