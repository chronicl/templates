<script lang="ts">
  import router from "page";
  import Home from "./pages/Home.svelte";
  import About from "./pages/About.svelte";
  import Navbar from "./components/Navbar2/Navbar.svelte";

  let page;

  router("/", () => (page = Home));
  router("/about", () => (page = About));

  router.start();
</script>

<style lang="scss">
  @import "styles/global.scss";
  @import "styles/theme.scss";

  @include not-phone {
    main {
      position: absolute;
      left: 72px;
      top: 0;
      width: calc(100% - 72px);
    }
  }
</style>

<Navbar />
<main>
  <svelte:component this={page} />
</main>
