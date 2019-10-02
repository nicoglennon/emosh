<script>
  import { spring } from "svelte/motion";

  let coords = spring(
    { x: 50, y: 50 },
    {
      stiffness: 0.05,
      damping: 0.1
    }
  );

  let size = spring(25);
</script>

<style>
  svg {
    width: 100%;
    height: 100%;
  }
  circle {
    animation: colorchange 10s infinite; /* animation-name followed by duration in seconds*/
    /* you could also use milliseconds (ms) or something like 2.5s */
    -webkit-animation: colorchange 10s infinite; /* Chrome and Safari */
  }

  @keyframes colorchange {
    0% {
      fill: red;
    }
    25% {
      fill: yellow;
    }
    50% {
      fill: blue;
    }
    75% {
      fill: green;
    }
    100% {
      fill: red;
    }
  }

  @-webkit-keyframes colorchange /* Safari and Chrome - necessary duplicate */ {
    0% {
      background: red;
    }
    25% {
      background: yellow;
    }
    50% {
      background: blue;
    }
    75% {
      background: green;
    }
    100% {
      background: red;
    }
  }
</style>

<svg
  on:mousemove={e => coords.set({ x: e.clientX, y: e.clientY })}
  on:mousedown={() => size.set(1000)}
  on:mouseup={() => size.set(25)}>
  <circle cx={$coords.x} cy={$coords.y} r={$size} />
</svg>
