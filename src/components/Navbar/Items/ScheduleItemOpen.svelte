<script lang="ts">
  import ItemOpen from './templates/ItemOpen.svelte';
  import Checkbox from '../../Checkbox.svelte';
  import { countdown, active, ampm } from '../../../stores';

  let href = '/schedule';
  $: isActive = $active === href;
</script>

<style lang="scss">
  @import '../../../styles/navbar.scss';

  .settings {
    margin-top: 5px;
    display: grid;
    padding-left: $closed-width;
    grid-template-columns: 35px auto;
    gap: 4px;

    :global(.checkbox) {
      align-self: center;
    }

    .label {
      align-self: center;
      font-size: $checkbox-text-size;
      color: $text;
      cursor: pointer;

      &.active {
        color: $active-text;
      }
    }
  }
</style>

<div class="ScheduleOpen">
  <ItemOpen text="Schedule" {href}>
    <svg viewBox="0 0 24 24">
      <g>
        <rect
          transform="scale(-1,1)"
          x="-23.795"
          y="2.2052"
          width="23.59"
          height="21.59"
          ry="2.0878"
          fill="none"
          stroke-width=".41045" />
        <g transform="translate(-.076425 -.21873)" stroke-width=".3626">
          <rect x="3.867" y="8.1173" width="2.6374" height="2.6374" />
          <rect x="8.4608" y="8.1173" width="2.6374" height="2.6374" />
          <rect x="13.055" y="8.1173" width="2.6374" height="2.6374" />
          <rect x="17.648" y="8.1173" width="2.6374" height="2.6374" />
        </g>
        <g transform="translate(-.076425 4.1562)" stroke-width=".3626">
          <rect x="3.867" y="8.1173" width="2.6374" height="2.6374" />
          <rect x="8.4608" y="8.1173" width="2.6374" height="2.6374" />
          <rect x="13.055" y="8.1173" width="2.6374" height="2.6374" />
          <rect x="17.648" y="8.1173" width="2.6374" height="2.6374" />
        </g>
        <g transform="translate(-.076425 8.5312)" stroke-width=".3626">
          <rect x="3.867" y="8.1173" width="2.6374" height="2.6374" />
          <rect x="8.4608" y="8.1173" width="2.6374" height="2.6374" />
          <rect x="13.055" y="8.1173" width="2.6374" height="2.6374" />
          <rect x="17.648" y="8.1173" width="2.6374" height="2.6374" />
        </g>
        <g transform="translate(-.30933)" stroke-width=".37795">
          <rect x="6.5161" y=".18898" width="1.2499" height="4" ry=".625" />
          <rect x="11.684" y=".18898" width="1.2499" height="4" ry=".625" />
          <rect x="16.853" y=".18898" width="1.2499" height="4" ry=".625" />
        </g>
      </g>
    </svg>
  </ItemOpen>
  <div class="settings">
    <Checkbox bind:value={$countdown} id="countdown" bind:active={isActive} />
    <label class="label {isActive ? 'active' : ''}" for="countdown">Countdown</label>
    <Checkbox bind:value={$ampm} id="ampm" bind:active={isActive} />
    <label class="label {isActive ? 'active' : ''}" for="ampm">AM / PM</label>
  </div>
</div>
