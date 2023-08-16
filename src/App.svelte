<script lang="ts">
  import router from "page"
  import Home from "./routes/Home.svelte"
  import Profile from "./routes/Profile.svelte"
  
  let page;
  let params;

  router("/", () => (page = Home));
  router("/profile", () => (page = Profile));
  
  router.start();
</script>

<svelte:component this="{page}" params="{params}" />