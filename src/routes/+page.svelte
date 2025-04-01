<script>
  import Sketch from "../Sketch.svelte";
</script>

<div>
  <Sketch />
  <div class="content">
    <h1>Welcome to My Page</h1>
    <p>This text appears above the animation</p>
  </div>
</div>

<style>
  :global(body) {
    background-color: #ffffea;
  }

  div {
    justify-content: center;
  }
  .content {
    position: absolute; /* Keeps text above the canvas */
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
    font-size: 2em;
    font-family: Arial, sans-serif;
    z-index: 10; /* Higher than the canvas */
  }
</style>
