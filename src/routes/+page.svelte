<script>
	import {dndzone} from 'svelte-dnd-action';
  import WebComponent from './WebComponent.svelte';

  const CELL_SIZE = 324;
  let items = [
    {"id": "alerts", "url": "http://localhost:5173/widgets/wc-alerts.js", "element": "wc-alerts", "size": {
      "min": {"h": 1, "w": 1}      
    }},
    {"id": "assets", "url": "http://localhost:5173/widgets/wc-assets.js", "element": "wc-assets", "size": {
      "min": {"h": 1, "w": 2}      
    }}
  ];
  	/**
   * @param {{ detail: { items: { id: string; url: string; element: string; size: { min: { h: number; w: number; }; }; }[]; }; }} e
   */
	function handleSort(e) {
		items = e.detail.items;
	}
  function transformDraggedElement(draggedEl) {
    draggedEl.style.cursor = 'move';
  }
</script>

<h1>Drag and Drop of Web Components, using
<a href="https://github.com/isaacHagoel/svelte-dnd-action">svelte-dnd-action</a></h1>
<section class="widget-container" use:dndzone={{items, transformDraggedElement}} on:consider={handleSort} on:finalize={handleSort}
  style="grid-template-columns: repeat(auto-fit, minmax({`${(CELL_SIZE + 6) * 2}px`}, 1fr)); min-height:{`${CELL_SIZE}px`}">
	{#each items as item(item.id)}
		<div class="widget">
      <WebComponent component={item}/>
		</div>
	{/each}
</section>

<style>
  .widget-container {
    width: 100%;
    float: left;
    margin: 0 auto;
    display: grid;
    gap: 33px;
  }
  .widget {
    background: var(--cds-ui-02);
    box-shadow: 0px 2px 1px -1px rgb(0 0 0 / 20%), 0px 1px 1px 0px rgb(0 0 0 / 14%), 0px 1px 3px 0px rgb(0 0 0 / 12%);
    font-family: 'TWK Everett';
    font-size: 14px;
    float: left;
  }
</style>