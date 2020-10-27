<script lang="ts">
  export let value: boolean;
  export let id: string = '';
  export let active: boolean = true;
</script>

<style lang="scss">
  @import '../styles/navbar.scss';

  .checkbox {
    position: relative;
    input,
    svg {
      width: 21px;
      height: 21px;
      display: block;
    }
    input {
      -webkit-appearance: none;
      -moz-appearance: none;
      position: relative;
      outline: none;
      background: $bgc;
      border: none;
      margin: 0;
      padding: 0;
      cursor: pointer;
      border-radius: 4px;
      transform: scale($checkbox-scale);
      transition: box-shadow 0s;
      box-shadow: inset 0 0 0 1px $text;

      &.active:hover {
        box-shadow: inset 0 0 0 1px $hover-text;
      }
      &.active:checked {
        box-shadow: inset 0 0 0 1px $active-text;
      }

      &:checked {
        & + svg {
          stroke-dasharray: 16.1 86.12;
          stroke-dashoffset: 102.22;
        }
      }
    }
    svg {
      pointer-events: none;
      fill: none;
      stroke-width: 2px;
      stroke-linecap: round;
      stroke-linejoin: round;
      stroke: $text;
      position: absolute;
      top: 0;
      left: 0;
      width: 21px;
      height: 21px;
      transform: scale($checkbox-scale) translateZ(0);
      stroke-dasharray: 86.12;
      stroke-dashoffset: 86.12;
      transition: stroke-dasharray 0.6s, stroke-dashoffset 0.6s;

      &.active {
        stroke: $active-text;
      }
    }
  }
</style>

<label class="checkbox path">
  <input class:active type="checkbox" bind:checked={value} {id} />
  <svg class:active viewBox="0 0 21 21">
    <path
      d="M5,10.75 L8.5,14.25 L19.4,2.3 C18.8333333,1.43333333 18.0333333,1 17,1 L4,1 C2.35,1 1,2.35 1,4 L1,17 C1,18.65 2.35,20 4,20 L17,20 C18.65,20 20,18.65 20,17 L20,7.99769186" />
  </svg>
</label>
