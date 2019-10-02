<script>
  import { spring } from "svelte/motion";
  import { fade } from "svelte/transition";

  let coords = spring(
    { x: 50, y: 50 },
    {
      stiffness: 0.05,
      damping: 0.1
    }
  );

  let size = spring(25);
  let visible = false;
</script>

<style>
  svg {
    width: 100%;
    height: 100%;
  }
  text {
    font-family: "Caveat", cursive;
    user-select: none;
    font-size: 30px;
  }
  text.title {
    font-size: 64px;
  }
  circle {
    animation: colorchange 10s infinite; /* animation-name followed by duration in seconds*/
    /* you could also use milliseconds (ms) or something like 2.5s */
    -webkit-animation: colorchange 10s infinite; /* Chrome and Safari */
  }

  @keyframes colorchange {
    0% {
      fill: #ff7675;
    }
    25% {
      fill: #fdcb6e;
    }
    50% {
      fill: #55efc4;
    }
    75% {
      fill: #a29bfe;
    }
    100% {
      fill: #fd79a8;
    }
  }

  @-webkit-keyframes colorchange /* Safari and Chrome - necessary duplicate */ {
    0% {
      fill: #ff7675;
    }
    25% {
      fill: #fdcb6e;
    }
    50% {
      fill: #55efc4;
    }
    75% {
      fill: #a29bfe;
    }
    100% {
      fill: #fd79a8;
    }
  }
</style>

<svg
  on:mousemove={e => coords.set({ x: e.clientX, y: e.clientY })}
  on:mousedown={() => {
    visible = true;
    size.set(1000);
  }}
  on:touchstart={e => {
    coords.set({ x: e.touches[0].clientX, y: e.touches[0].clientY });
    visible = true;
    size.set(1000);
  }}
  on:mouseup={() => {
    visible = false;
    size.set(25);
  }}
  on:touchend={() => {
    visible = false;
    size.set(25);
  }}>
  <circle cx={$coords.x} cy={$coords.y} r={$size} />
  {#if visible}
    <g transition:fade>
      <text
        class="title"
        x="50%"
        y="47%"
        dominant-baseline="middle"
        text-anchor="middle"
        fill="white">
        emosh
      </text>
      <text
        class="subtitle"
        x="50%"
        y="52%"
        dominant-baseline="middle"
        text-anchor="middle"
        fill="white">
        coming soon(ish)
      </text>
    </g>
  {/if}

</svg>
