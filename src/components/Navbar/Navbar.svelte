<script lang="ts">
  import Burger from "./Burger.svelte";
  import ScheduleItemOpen from "./Items/ScheduleItemOpen.svelte";
  import ScheduleItemClosed from "./Items/ScheduleItemClosed.svelte";
  import HomeItemOpen from "./Items/HomeItemOpen.svelte";
  import HomeItemClosed from "./Items/HomeItemClosed.svelte";

  import { open } from "../../stores";

  import { onMount } from "svelte";
  import { fade } from "svelte/transition";

  let mobile = false;
  onMount(() => {
    if (window.innerHeight < 768) {
      mobile = true;
    }
  });
</script>

<style lang="scss">
  @import "../../styles/navbar.scss";

  .Navbar {
    position: fixed;
    top: 0;
    left: 0;
    overflow: visible;
    z-index: 100;

    .items {
      position: relative;
      background-color: $bgc;
      height: 100vh;
      width: $open-width;
      z-index: 101;
      padding-top: 50px;
      transform: translate3d(calc(#{$closed-width} - #{$open-width}), 0, 0);
      @include transition($transition);

      &.open {
        transform: translate3d(0, 0, 0);
      }

      .closedItems,
      .openItems {
        position: absolute;
        left: 0;
        top: $items-top;
        width: 100%;
        display: flex;
        flex-direction: column;
      }
    }

    :global(.Burger) {
      margin-bottom: 3px;
      position: fixed;
      left: 0;
      top: 0;
      transform: translate(calc((#{$closed-width} - 100%) / 2), 5px);
      z-index: 102;
    }
  }
</style>

<nav class="Navbar">
  <!-- {#if !mobile} -->
  <Burger />
  <!-- {/if} -->

  <div class="items {$open ? 'open' : ''}">
    <div class="openItems">
      {#if $open}
        <div
          in:fade={{ delay: 200, duration: 200 }}
          out:fade={{ duration: 200 }}>
          <HomeItemOpen />
          <ScheduleItemOpen />
        </div>
      {/if}
    </div>
    <div class="closedItems">
      {#if !$open}
        <div
          in:fade={{ delay: 200, duration: 200 }}
          out:fade={{ duration: 200 }}>
          <HomeItemClosed />
          <ScheduleItemClosed />
        </div>
      {/if}
    </div>
  </div>
</nav>
