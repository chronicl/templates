<script lang="ts">
  import { onMount } from "svelte";

  export let text: string;
  export let href: string;

  import { active } from "../../../../stores";

  onMount(() => {
    $active = window.location.pathname;
  });

  function handleClick() {
    $active = href;
  }
</script>

<style lang="scss">
  @import "../../../../styles/navbar.scss";

  a {
    width: 100%;
  }
  .Item {
    position: relative;
    width: 100%;
    color: $text;

    .grid {
      margin-left: calc(#{$open-width} - #{$closed-width});
      width: $closed-width;
      display: grid;
      grid-template-rows: $svg-size auto;
      padding: $closed-padding;

      &:hover {
        background-color: $hover-bgc;
        color: $hover-text;
      }

      &.active {
        background-color: $active-bgc;
        color: $hover-text;
      }

      :global(svg) {
        justify-self: center;
        align-self: end;
        width: $svg-size;
        height: $svg-size;
        fill: none;
        stroke: $active-text;
      }

      &.active,
      &:hover > {
        :global(svg) {
          fill: $svgc;
        }
      }

      .text {
        padding-top: $text-padding-top;
        justify-self: center;
        align-self: center;
        font-size: 11px;
        text-align: center;
      }
    }
  }
</style>

<a {href} on:click={handleClick}>
  <div class="Item {text}">
    <div class="grid {$active === href ? 'active' : ''}">
      <slot />
      <div class="text">{text}</div>
    </div>
  </div>
</a>
