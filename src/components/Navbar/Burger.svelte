<script lang="ts">
  import { open } from '../../stores';

  import { tweened } from 'svelte/motion';
  import { cubicOut, linear } from 'svelte/easing';

  let duration = 500;
  const interpolateI1_2 = (
    from: { width: number; opacity: number },
    to: { width: number; opacity: number }
  ) => {
    if (from.opacity === 1) {
      return t => {
        if (t <= 0.5)
          return {
            width: from.width + (to.width - from.width) * t * 2,
            opacity: from.opacity + (to.opacity - from.opacity) * t * 2,
          };
        else return { width: to.width, opacity: to.opacity };
      };
    } else {
      return t => {
        if (t <= 0.5) return { width: from.width, opacity: from.opacity };
        else
          return {
            width: from.width + (to.width - from.width) * (t - 0.5) * 2,
            opacity: from.opacity + (to.opacity - from.opacity) * (t - 0.5) * 2,
          };
      };
    }
  };
  const i1_2 = tweened(
    { width: 24, opacity: 1 },
    {
      duration,
      easing: linear,
      interpolate: interpolateI1_2,
    }
  );

  const interpolateI3_4 = (from: { width: number; deg: number }, to: { width: number; deg: number }) => {
    if (from.width < to.width) {
      return t => {
        if (t <= 0.5) return { width: from.width + (to.width - from.width) * t * 2, deg: from.deg };
        else return { width: to.width, deg: from.deg + (to.deg - from.deg) * (t - 0.5) * 2 };
      };
    } else {
      return t => {
        if (t <= 0.5) return { width: from.width, deg: from.deg + (to.deg - from.deg) * t * 2 };
        else return { width: from.width + (to.width - from.width) * (t - 0.5) * 2, deg: to.deg };
      };
    }
  };
  const i3 = tweened(
    { width: 24, deg: 0 },
    {
      duration,
      easing: linear,
      interpolate: interpolateI3_4,
    }
  );
  const i4 = tweened(
    { width: 24, deg: 0 },
    {
      duration,
      easing: linear,
      interpolate: interpolateI3_4,
    }
  );
</script>

<style lang="scss">
  @import '../../styles/theme.scss';

  .hamburger-button {
    padding: 8px;
    border: 0;
    border-radius: 8px;
    background-color: $dark-middle;
    outline: none;
    cursor: pointer;
    transition: 0.3s ease-in-out;
  }
  .hamburger-button:hover {
    background-color: $dark-middle-light;
  }
  .hamburger-button .icon {
    position: relative;
    display: block;
    width: 24px;
    height: 24px;
  }
  .hamburger-button .icon i {
    position: absolute;
    width: 24px;
    height: 4px;
    border-radius: 2px;
    background-color: #ffffff;
    animation-duration: 0.6s;
    animation-fill-mode: forwards;
    animation-direction: reverse;
  }
  .hamburger-button .icon i:nth-child(1) {
    left: 0;
    top: 0;
  }
  .hamburger-button .icon i:nth-child(2) {
    right: 0;
    bottom: 0;
  }
  .hamburger-button .icon i:nth-child(3),
  .hamburger-button .icon i:nth-child(4) {
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
  }
</style>

<div class="Burger">
  <button
    class="hamburger-button"
    on:click={() => {
      $open = !$open;
      if ($open) {
        i1_2.set({ width: 0, opacity: 0 });
        i3.set({ width: 32, deg: 45 });
        i4.set({ width: 32, deg: -45 });
      } else {
        i1_2.set({ width: 24, opacity: 1 });
        i3.set({ width: 24, deg: 0 });
        i4.set({ width: 24, deg: 0 });
      }
    }}>
    <span class="icon">
      <i style="width: {$i1_2.width}px; opacity: {$i1_2.opacity}" />
      <i style="width: {$i1_2.width}px; opacity: {$i1_2.opacity}" />
      <i style="width: {$i3.width}px; transform: translate(-50%, -50%) rotate({$i3.deg}deg)" />
      <i style="width: {$i4.width}px; transform: translate(-50%, -50%) rotate({$i4.deg}deg)" />
    </span>
  </button>
</div>
