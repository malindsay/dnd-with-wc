<script>
  import { onMount } from 'svelte';

	/**
   * @type {{ element: any; url: string; }}
   */
	 export let component;

  $:Components = undefined;
  onMount(async () => {
    console.log('WebComponent onMount (loading): ',  component.element); 
    await import( /* @vite-ignore */ component.url);
  });

  function onLoad() {
    console.log('WebComponent onLoad: ',  component.element); 

  }
</script>
<svelte:element this={component.element} use:onLoad></svelte:element>