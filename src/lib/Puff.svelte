<script lang="ts">
  import type { SpinnerTypes } from './types/spinner.type'
  import { range, durationUnitRegex, calculateRgba } from './utils'
  export let color: SpinnerTypes['color'] = '#FF3E00'
  export let unit: SpinnerTypes['unit'] = 'px'
  export let duration: SpinnerTypes['duration'] = '1s'
  export let size: SpinnerTypes['size'] = '60'
  export let pause: SpinnerTypes['pause'] = false
  let durationUnit: string = duration.match(durationUnitRegex)?.[0] ?? 's'
  let durationNum: string = duration.replace(durationUnitRegex, '')
  let rgba: string
  $: rgba = calculateRgba(color, 1)
</script>

<span
  class="wrapper"
  style="--size: {size}{unit}; --color: {color}; --rgba: {rgba}; --duration: {duration}"
>
  {#each range(2, 1) as version}
    <span
      class="circle"
      class:pause-animation={pause}
      style="animation-delay: {version === 1
        ? '-1s'
        : '0s'}; animation-duration: {2 / +durationNum + durationUnit};"
    />
  {/each}
</span>

<style>
  .wrapper {
    display: inherit;
    position: relative;
    width: var(--size);
    height: var(--size);
  }
  .circle {
    position: absolute;
    width: var(--size);
    height: var(--size);
    border: thick solid var(--rgba);
    border-radius: 50%;
    opacity: 1;
    top: 0px;
    left: 0px;
    animation-fill-mode: both;
    animation-iteration-count: infinite;
    animation-timing-function: cubic-bezier(0.165, 0.84, 0.44, 1),
      cubic-bezier(0.3, 0.61, 0.355, 1);
    animation-direction: normal, normal;
    animation-fill-mode: none, none;
    animation-play-state: running, running;
    animation-name: puff-1, puff-2;
    box-sizing: border-box;
  }
  .pause-animation {
    animation-play-state: paused;
  }
  @keyframes puff-1 {
    0% {
      transform: scale(0);
    }
    100% {
      transform: scale(1);
    }
  }
  @keyframes puff-2 {
    0% {
      opacity: 1;
    }
    100% {
      opacity: 0;
    }
  }
</style>
