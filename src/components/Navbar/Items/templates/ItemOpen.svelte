<script lang="ts">
  import { onMount } from 'svelte';

  export let text: string;
  export let href: string;

  import { active } from '../../../../stores';

  onMount(() => {
    $active = window.location.pathname;
  });

  function handleClick() {
    $active = href;
  }
</script>

<style lang="scss">
  @import '../../../../styles/navbar.scss';

  a {
    width: 100%;
  }
  .Item {
    position: relative;
    width: 100%;
    color: $text;

    .grid {
      width: 100%;
      display: grid;
      grid-template-columns: $closed-width auto;
      padding: $open-padding;

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
        align-self: center;
      }
    }
  }
</style>

<a {href} on:click={handleClick}>
  <div class="Item">
    <div class="grid {$active === href ? 'active' : ''}">
      <slot />
      <div class="text">{text}</div>
    </div>
  </div>
</a>
