<script lang="ts">
  import type { Circle2Types } from './types/spinner.type'
  export let size: Circle2Types['size'] = '60'
  export let unit: Circle2Types['unit'] = 'px'
  export let pause: Circle2Types['pause'] = false
  export let colorOuter: Circle2Types['colorOuter'] = '#FF3E00'
  export let colorCenter: Circle2Types['colorCenter'] = '#40B3FF'
  export let colorInner: Circle2Types['colorInner'] = '#676778'
  export let durationMultiplier: Circle2Types['durationMultiplier'] = 1
  export let durationOuter: Circle2Types['durationOuter'] = `${durationMultiplier * 2}s`
  export let durationInner: Circle2Types['durationInner'] = `${durationMultiplier * 1.5}s`
  export let durationCenter: Circle2Types['durationCenter'] = `${durationMultiplier * 3}s`
</script>

<div
  class="circle"
  class:pause-animation={pause}
  style="--size: {size}{unit}; --colorInner: {colorInner}; --colorCenter: {colorCenter}; --colorOuter: {colorOuter}; --durationInner: {durationInner}; --durationCenter: {durationCenter}; --durationOuter: {durationOuter};"
/>

<style>
  .circle {
    width: var(--size);
    height: var(--size);
    box-sizing: border-box;
    position: relative;
    border: 3px solid transparent;
    border-top-color: var(--colorOuter);
    border-radius: 50%;
    animation: circleSpin var(--durationOuter) linear infinite;
  }
  .circle::before,
  .circle::after {
    content: '';
    box-sizing: border-box;
    position: absolute;
    border: 3px solid transparent;
    border-radius: 50%;
  }
  .circle::after {
    border-top-color: var(--colorInner);
    top: 9px;
    left: 9px;
    right: 9px;
    bottom: 9px;
    animation: circleSpin var(--durationInner) linear infinite;
  }
  .circle::before {
    border-top-color: var(--colorCenter);
    top: 3px;
    left: 3px;
    right: 3px;
    bottom: 3px;
    animation: circleSpin var(--durationCenter) linear infinite;
  }
  .pause-animation,
  .pause-animation::after,
  .pause-animation::before {
    animation-play-state: paused;
  }

  @keyframes circleSpin {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
</style>
