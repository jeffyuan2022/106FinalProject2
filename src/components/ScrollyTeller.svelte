<script>
  import Scroller from "@sveltejs/svelte-scroller";
  import Introduction from "./Introduction.svelte";
  import Graph from "./Graph.svelte";
  import Income from "./Income.svelte";
  import USMap from "./USMap.svelte";
  // import 'daisyui/dist/full.css';
  let count, index, offset, progress;
</script>
<div class="box">
  <div class="range">
    <input type="range" min="0" max="100" value="70" class="range range-primary range-xs" />
  </div>
  
</div>
<style>
.box{
  width: 100%;
  height: 100px;
  padding: 20px 1%;
  display: flex;
  justify-content: start;
  align-items: center;
}
.range{
  width: 50%;
}
</style>
